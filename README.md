package com.ad;

import java.sql.*;

public class SqlOperation {

	public static void main(String[] args) throws Exception {
		
		String url ="jdbc:mysql://localhost:3306/film";
		String uname = "root";
		String pass = "Admin@pass" ;
				
			  Class.forName("com.mysql.cj.jdbc.Driver");
			  
			  // here database name is url, username is uname and password = pass
			  Connection con = DriverManager.getConnection(url,uname,pass);
				  String query =
				  " insert into Movies (ReleaseYear, MovieName, LeadActor, LeadActress, DirectorName)"
				  + " values (?, ?, ?, ?, ?)";
				  
				  // create the mysql insert preparedstatement 
				  PreparedStatement preparedStmt = con.prepareStatement(query); 
				  preparedStmt.setInt(1, 2021);
				  preparedStmt.setString(2, "Sooryavanshi"); 
				  preparedStmt.setString(3,"Akshay Kumar"); 
				  preparedStmt.setString(4, "Katrina Kaif");
				  preparedStmt.setString(5, "Rohit Shetty");
				  
				  // execute the preparedstatement 
				 int count = preparedStmt.executeUpdate();
				System.out.println(count +"Rows Affected\n");

			  // create statement
			  Statement stmt = con.createStatement();
			  // create resultset to display result of the query
			  ResultSet rs = stmt.executeQuery("select * from movies");
              
			  System.out.println("RelYear\t" + "MovieName\t"+"LeadActor\t" + " LeadActress\t" + "DirectorName");
			  while (rs.next()) {
				System.out.println(rs.getInt(1) +"\t"+ rs.getString(2) +"\t"+ rs.getString(3) +"\t"+ rs.getString(4) + "\t" + rs.getString(5));
			  }
			  
			  System.out.println("Fetching records with condition...");
		         String sql = "SELECT MovieName FROM Movies " +
		            " WHERE ReleaseYear>=2018";
		       rs = stmt.executeQuery(sql);
		       while(rs.next()) {
		    	   System.out.println(rs.getString("Moviename"));
		    	   
		       }
			  stmt.close();
			  con.close();
		
	}

}

