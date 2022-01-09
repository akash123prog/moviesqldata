package com.ad;

import java.beans.Statement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;

public class SqlData {

	public static void main(String[] args) throws Exception {
	 
	try {
		Class.forName("com.mysql.cj.jdbc.Driver");  
		Connection con=DriverManager.getConnection(  
		"jdbc:mysql://localhost:3306/film","root","Admin@pass");  
		//here film is database name, root is username and password = Admin@pass 
		String query = " insert into users (ReleaseYear, MovieName, LeadActor, LeadActress, DirectorName)"
		        + " values (?, ?, ?, ?, ?)";

		      // create the mysql insert preparedstatement
		      PreparedStatement preparedStmt = conn.prepareStatement(query);
		      preparedStmt.setInt (1, 2021);
		      preparedStmt.setString(2, "Sooryavanshi");
		      preparedStmt.setString(3, "Akshay Kumar");
		      preparedStmt.setString(4, "Katrina Kaif");
		      preparedStmt.setString(5, "Rohit Shetty");

		      // execute the preparedstatement
		      preparedStmt.execute();
 
		//create statement
		Statement stmt=(Statement) con.createStatement();
		//create resultset to display result of the query
		ResultSet rs= ((java.sql.Statement) stmt).executeQuery("select MovieName from Movies where LeadActor=Prabhas);  
		
		ResultSet rs= ((java.sql.Statement) stmt).executeQuery("select * from Movies);  
		while(rs.next())  
		System.out.println(rs.getInt(1)+"  "+rs.getString(2)+"  "+rs.getString(3)+" "+rs.getString(4)+" "+rs.getString(5));  
		
		con.close();  
		}catch(Exception e) 
	     { System.out.println(e);}   
	

	}

}
