## Ways to implement some stuffs

* Example on how to implement the _Insertion of a data in DB_ by JDBC

```
public class Program {
	
	public static void main(String[] args) {
		
        SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
		Connection conn = null;
		PreparedStatement st = null;

        try {
            conn = DB.getConnection();
            st = conn.prepareStatement(
                "INSERT INTO seller "
                + "(Name, Email, BirthDate, BaseSalary, DepartmentId) "
                + "VALUES "
                + "(?, ?, ?, ?, ?)"
            );
            st.setString(1, "Carl Purple");
            st.setString(2, "carl@gmail.com");
            st.setDate(3, new java.sql.Date(sdf.parse("13/07/1995").getTime()))
            st.setDouble(4, 3000.0);
            st.setInt(5,4);

            /*
            st = conn.prepareStatement("INSERT INTO department (Name) values ('D1'), ('D2')",
					Statement.RETURN_GENERATED_KEYS);
            */
            //When we need to see the data, we execute this command below
			int rowsAffected = st.executeUpdate();

			if (rowsAffected > 0) {
				ResultSet rs = st.getGeneratedKeys();
				while (rs.next()) {
					int id = rs.getInt(1);
				}
			} else {
				System.out.println("No rows affected!");
			}

            System.out.println("Done! Rows affected: " + rowsAffected);
        }
        catch (SQLException e){
            e.printStackTrace();
        }
        catch (ParseException e) {
            e.printStackTrace();
        }
        finally {
            DB.closeStatement(st);
            DB.closeConnection();
        }
	}
}
```

* Example of How to implement the _Update of a data in DB_ using JDBC

```
public class Program {
	
	public static void main(String[] args) {
		
		Connection conn = null;
		PreparedStatement st = null;
		try {
			conn = DB.getConnection();
			
			st = conn.prepareStatement(
					"UPDATE seller "
					+ "SET BaseSalary = BaseSalary + ? "
					+ "WHERE "
					+ "(DepartmentId = ?)"
					);
			st.setDouble(1, 200.00);
			st.setInt(2, 2);
			
			int rowsAffected = st.executeUpdate();
			
			System.out.println("Done! " + rowsAffected);
					
		} 
		catch(SQLException e) {
			e.printStackTrace();
		}
		finally {
			DB.closeStatement(st);
			DB.closeConnection();
		}
		
	}
}
```

