# JDBC-CRUD-OPERATIONS
# Connectivity to database and perform crud operations from Eclipse itself.
package jdbcMaven;
import java.sql.Statement;
import java.util.Scanner;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Connection;
public class Projectjdbc {
	public static void main(String[] args) {
		AllOperation op=new AllOperation();
		op.create();
		op.insert();
		op.read();
		op.update();
		op.delete();
	}		
}
class AllOperation{
	//CREATION OF TABLE
	public void create() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/PROJECT", "root", "1234");
			Statement st=con.createStatement();
			st.executeUpdate("CREATE TABLE CRUD(STID INT,STNAME VARCHAR(15),STCOURSE VARCHAR(15),STPSD VARCHAR(20))");
			System.out.println("TABLE CREATION COMPLETED.");
			System.out.println("-------------------------------------------------------------------");
			st.close();
			con.close();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public void insert() {
		Scanner s=new Scanner(System.in);
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/PROJECT", "root", "1234");
			PreparedStatement pst=con.prepareStatement("INSERT INTO CRUD VALUES(?,?,?,?)");
			System.out.println("ENTER THE VALUES TO INSERT IN  A TABLE");
			System.out.println("ENTER HOW MANY RECORDS TO INSERT:");
			int a=s.nextInt();
			for(int i=1;i<=a;i++) {
				System.out.println("ENTER THE STID");
				int b=s.nextInt();
				System.out.println("ENTER THE STNAME");
				String c=s.next();
				System.out.println("ENTER THE STCOURSE");
				String d=s.next();
				System.out.println("ENTER THE STPSD");
				String e=s.next();
				
				pst.setInt(1, b);
				pst.setString(2, c);
				pst.setString(3, d);
				pst.setString(4, e);
				
				int rows=pst.executeUpdate();
				System.out.println("ROWS EFFECTED="+rows);
			}
			System.out.println();
			System.out.println("-------------------------------------------------------------------");
			pst.close();
			con.close();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public void read() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/PROJECT", "root", "1234");
			PreparedStatement pst=con.prepareStatement("SELECT*FROM CRUD");
			ResultSet rst=pst.executeQuery();
			System.out.println("READING THE ELEMENTS IN CRUD");
			while(rst.next()) {
				System.out.println(rst.getInt(1));
				System.out.println(rst.getString(2));
				System.out.println(rst.getString(3));
				System.out.println(rst.getString(4));
			}
			System.out.println();
			System.out.println("-------------------------------------------------------------------");
			rst.close();
			pst.close();
			con.close();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public void update() {
		Scanner s=new Scanner(System.in);
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/PROJECT", "root", "1234");
			PreparedStatement pst=con.prepareStatement("UPDATE CRUD SET STPSD=? WHERE STID=?");
			System.out.println("ENTER HOW MANY RECORDS TO UPDATE.");
			int b=s.nextInt();
				for(int i=1;i<=b;i++) {
					System.out.println("ENTER THE STID WHERE TO UPDATE:");
					int a=s.nextInt();
//					System.out.println("ENTER THE PSD TO UPDATE:");
					String c=s.next();
					pst.setInt(2, a);
					pst.setString(1, c);
					int rowsEffected=pst.executeUpdate();
					System.out.println("Rows Effected="+rowsEffected);
		}
				System.out.println();
				System.out.println("-------------------------------------------------------------------");
				pst.close();
				con.close();
	}
		  catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public void delete() {
		Scanner s=new Scanner(System.in);
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/PROJECT", "root", "1234");
			PreparedStatement pst=con.prepareStatement("DELETE FROM CRUD WHERE STID=?");
			System.out.println("ENTER HOW MANY RECORDS TO DELETE.");
			int a=s.nextInt();
			for(int i=1;i<=a;i++) {
				System.out.println("ENTER STID TO DELETE:");
				int b=s.nextInt();
				pst.setInt(1, b);
				int rowsEffected=pst.executeUpdate();
				System.out.println("RowsEffected="+rowsEffected);
			}
			System.out.println();
			System.out.println("-------------------------------------------------------------------");
			pst.close();
			con.close();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}		
}
