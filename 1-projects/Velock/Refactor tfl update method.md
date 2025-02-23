# Refactor Tfl Update Method
Alright, let's craft that raw SQL query using `COALESCE` to handle those potential missing values. This approach will make our update more robust and prevent crashes due to invalid syntax.

TypeScript

```
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

async function refreshTable(updatedData: any[]) {
  try {
    // 1. Extract column names (excluding 'id')
    const columns = Object.keys(updatedData[0]).filter(key => key !== 'id')

    // 2. Construct the SQL query dynamically with COALESCE
    const sql = `
      UPDATE your_table_name
      SET ${columns.map(col => `${col} = COALESCE('${data[col]}', ${col})`).join(', ')}
      WHERE id = ${data.id};
    `

    await prisma.$queryRawUnsafe(sql)

    console.log('Table refreshed successfully!')
  } catch (error) {
    console.error('Error refreshing table:', error)
  }
}
```

**Explanation**

- We're still using `$queryRawUnsafe` to execute a raw SQL query.
    
- The `COALESCE` function is the star here. For each column, it checks if the corresponding value in `updatedData` (`${data[col]}`) is missing.
    
    - If the value is missing, `COALESCE` will retain the original value of that column in the database (`col`).
        
    - If the value is present, it will be used for the update.

**Important Notes**

- **Replace `your_table_name`**: Don't forget to use your actual table name.
    
- **Data Types**: The code assumes string values. Adjust the query if you have other data types (e.g., remove the single quotes for numbers).
    
- **SQL Injection**: If `updatedData` comes from external sources, sanitize the input to prevent SQL injection.
    
- **Prepare `updatedData`**: This should be an array of objects, with each object representing a row and containing the updated values (or `undefined` for missing values).

This approach ensures that even with missing values in your `updatedData`, the update operation will execute smoothly without any syntax errors.