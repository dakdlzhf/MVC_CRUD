

model/MemoDAO

```java
package model;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;

import model.MemoDTO;
import utility.DBClose;
import utility.DBOpen;

public class MemoDAO {

	public boolean create(MemoDTO dto) {
		boolean flag = false;

		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;

		StringBuffer sql = new StringBuffer();
		sql.append(
				" insert into memo (wname, title, content, wdate, grpno, passwd) values (?,?,?,sysdate(),(select ifnull(max(grpno),0) + 1 from memo m), ?) ");

		try {
			pstmt = con.prepareStatement(sql.toString());

			pstmt.setString(1, dto.getWname());
			pstmt.setString(2, dto.getTitle());
			pstmt.setString(3, dto.getContent());
			pstmt.setString(4, dto.getPasswd());

			int cnt = pstmt.executeUpdate();

			if (cnt > 0) {
				flag = true;
			}

		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			DBClose.close(pstmt, con);
		}

		return flag;
	}
	
	public boolean createReply(MemoDTO dto) {
		boolean flag = false;
		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		StringBuffer sql = new StringBuffer();
		sql.append(	" INSERT INTO memo(wname,title,content,passwd,wdate,grpno,indent,ansnum) ") ;
		sql.append(" values(?,?,?,?,sysdate(),?,?,? ) ") ;

		try {
			pstmt = con.prepareStatement(sql.toString());
			pstmt.setString(1, dto.getWname());
			pstmt.setString(2, dto.getTitle());
			pstmt.setString(3, dto.getContent());
			pstmt.setString(4, dto.getPasswd());
			pstmt.setInt(5, dto.getGrpno());
			pstmt.setInt(6, dto.getIndent()+1);
			pstmt.setInt(7, dto.getAnsnum()+1);

			int cnt = pstmt.executeUpdate();
			if (cnt > 0)
				flag = true;

		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			DBClose.close(pstmt, con);
		}
		return flag;
	}
	
	public void upAnsnum(Map map) {
		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		StringBuffer sql = new StringBuffer();
		sql.append(" update memo ");
		sql.append(" set ");
		sql.append(" ansnum = ansnum + 1 ");
		sql.append(" where grpno = ? and ansnum > ? ");
		
		int grpno = (int)map.get("grpno");
		int ansnum = (int)map.get("ansnum");
		
		
		try {
			pstmt =con.prepareStatement(sql.toString());
			pstmt.setInt(1, grpno);
			pstmt.setInt(2, ansnum);
			
			pstmt.executeUpdate();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}finally {
			DBClose.close(pstmt, con);
		}
		
	}
	
	public MemoDTO readReply(int memono) {
		MemoDTO dto = null;
		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		ResultSet rs = null;

		StringBuffer sql = new StringBuffer();
		sql.append(" SELECT memono,title,grpno,indent,ansnum ");
		sql.append(" FROM memo ");
		sql.append(" WHERE memono = ? ");

		try {
			pstmt = con.prepareStatement(sql.toString());
			pstmt.setInt(1, memono);
			rs = pstmt.executeQuery();

			if (rs.next()) {
				dto = new MemoDTO();
				dto.setMemono(rs.getInt("memono"));
				dto.setTitle(rs.getString("title"));
				dto.setGrpno(rs.getInt("grpno"));
				dto.setIndent(rs.getInt("indent"));
				dto.setAnsnum(rs.getInt("ansnum"));
			}
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			DBClose.close(rs, pstmt, con);
		}

		return dto;
	}
	
	public boolean passCheck(Map map) {
		boolean flag = false;

		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		ResultSet rs = null;

		int memono = (int) map.get("memono");
		String passwd = (String) map.get("passwd");

		StringBuffer sql = new StringBuffer();

		sql.append(" SELECT count(memono) as cnt ");
		sql.append(" FROM memo ");
		sql.append(" WHERE memono = ?  ");
		sql.append(" and passwd = ? ");

		try {
			pstmt = con.prepareStatement(sql.toString());
			pstmt.setInt(1, memono);
			pstmt.setString(2, passwd);

			rs = pstmt.executeQuery();

			rs.next();
			int cnt = rs.getInt("cnt");

			if (cnt > 0) {
				flag = true;

			}

		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			DBClose.close(rs, pstmt, con);
		}

		return flag;
	}
	
	public void upviewcnt(int memono) {
		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;

		StringBuffer sql = new StringBuffer();
		sql.append(" update memo ");
		sql.append(" set viewcnt = viewcnt + 1 ");
		sql.append(" where memono = ? ");

		try {
			pstmt = con.prepareStatement(sql.toString());
			pstmt.setInt(1, memono);
			pstmt.executeUpdate();

		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			DBClose.close(pstmt, con);
		}

	}
	
	public boolean update(MemoDTO dto) {
		boolean flag = false;

		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		StringBuffer sql = new StringBuffer();

		sql.append(" UPDATE memo ");
		sql.append(" set ");
		sql.append(" wname = ? , ");
		sql.append(" title = ? , ");
		sql.append(" content = ?  ");
		sql.append(" WHERE memono = ? ");

		try {
			pstmt = con.prepareStatement(sql.toString());
			pstmt.setString(1, dto.getWname());
			pstmt.setString(2, dto.getTitle());
			pstmt.setString(3, dto.getContent());
			pstmt.setInt(4, dto.getMemono());

			int cnt = pstmt.executeUpdate();
			if (cnt > 0) {
				flag = true;
			}

		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			DBClose.close(pstmt, con);
		}

		return flag;
	}
	
	public boolean delete(int bbsno) {
		boolean flag = false;
		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		StringBuffer sql = new StringBuffer();
		sql.append(" delete from memo ");
		sql.append(" where memono = ? ");

		try {
			pstmt = con.prepareStatement(sql.toString());
			pstmt.setInt(1, bbsno);

			int cnt = pstmt.executeUpdate();
			if (cnt > 0)
				flag = true;

		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			DBClose.close(pstmt, con);
		}

		return flag;
	}


	public MemoDTO read(int memono) {
		MemoDTO dto = null;
		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		ResultSet rs = null;
		StringBuffer sql = new StringBuffer();

		sql.append(" SELECT wname,title,content,passwd,viewcnt,wdate,grpno,indent,ansnum ");
		sql.append(" FROM memo WHERE memono = ? ");

		try {
			pstmt = con.prepareStatement(sql.toString());
			pstmt.setInt(1, memono);
			rs = pstmt.executeQuery();

			if (rs.next()) {
				dto = new MemoDTO();
				dto.setWname(rs.getString("wname"));
				dto.setTitle(rs.getString("title"));
				dto.setContent(rs.getString("content"));
				dto.setPasswd(rs.getString("passwd"));
				dto.setViewcnt(rs.getString("viewcnt"));
				dto.setWdate(rs.getString("wdate"));
				dto.setGrpno(rs.getInt("grpno"));
				dto.setIndent(rs.getInt("indent"));
				dto.setAnsnum(rs.getInt("ansnum"));
			}

		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			DBClose.close(rs, pstmt, con);
		}
		return dto;

	}

	public List<MemoDTO> list(Map map) {
		List<MemoDTO> list = new ArrayList<MemoDTO>();

		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		ResultSet rs = null;
		StringBuffer sql = new StringBuffer();

		String col = (String) map.get("col");
		String word = (String) map.get("word");

		int sno = (int) map.get("sno"); // 레코드 시작위치
		int eno = (int) map.get("eno"); // 가져올 건수

		sql.append(" SELECT * FROM memo ");

		if (word.trim().length() > 0 && col.equals("title_content")) {
			sql.append(" where title like concat('%' , ? , '%')  ");
			sql.append(" or content like concat('%' , ? , '%')  ");
		} else if (word.trim().length() > 0) {
			sql.append(" where " + col + " like concat('%' , ? , '%')  ");
		}

		sql.append(" order by grpno desc, ansnum ASC ");
		sql.append(" limit ?,? ");

		int i = 0;

		try {
			pstmt = con.prepareStatement(sql.toString());

			if (word.trim().length() > 0 && col.equals("title_content")) {
				pstmt.setString(++i, word);
				pstmt.setString(++i, word);
			} else if (word.trim().length() > 0) {
				pstmt.setString(++i, word);
			}
			pstmt.setInt(++i, sno);
			pstmt.setInt(++i, eno);

			rs = pstmt.executeQuery();

			while (rs.next()) {

				MemoDTO dto = new MemoDTO();
				dto.setMemono(rs.getInt("memono"));
				dto.setWname(rs.getString("wname"));
				dto.setTitle(rs.getString("title"));
				dto.setContent(rs.getString("content"));
				dto.setPasswd(rs.getString("passwd"));
				dto.setWdate(rs.getString("wdate"));
				dto.setGrpno(rs.getInt("grpno"));
				dto.setIndent(rs.getInt("indent"));
				dto.setAnsnum(rs.getInt("ansnum"));

				list.add(dto);
			}

		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			DBClose.close(rs, pstmt, con);
		}

		return list;
	}

	public int total(Map map) {
		int total = 0;
		Connection con = DBOpen.getConnection();
		PreparedStatement pstmt = null;
		ResultSet rs = null;
		StringBuffer sql = new StringBuffer();

		String col = (String) map.get("col");
		String word = (String) map.get("word");

		sql.append(" SELECT count(*) from memo ");

		if (word.trim().length() > 0 && col.equals("title_content")) {
			sql.append(" where title like concat('%' , ? , '%')  ");
			sql.append(" or content like concat('%' , ? , '%')  ");
		} else if (word.trim().length() > 0) {
			sql.append(" where " + col + " like concat('%' , ? , '%')  ");
		}

		try {
			pstmt = con.prepareStatement(sql.toString());
			if (word.trim().length() > 0 && col.equals("title_content")) {
				pstmt.setString(1, word);
				pstmt.setString(2, word);
			} else if (word.trim().length() > 0) {
				pstmt.setString(1, word);
			}

			rs = pstmt.executeQuery();
			if (rs.next()) {
				total = rs.getInt(1);
			}
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			DBClose.close(rs, pstmt, con);
		}
		return total;
	}
}

```

