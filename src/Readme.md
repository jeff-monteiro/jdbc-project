## Ways to implement some stuffs

* Example on how to implement the _Insertion of data_ by JDBC

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

            //When we need to change the data, we execute this command below
            int rowsAffected = st.executeUpdate();

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

