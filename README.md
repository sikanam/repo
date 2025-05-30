# Title: Excel Column Comparison Tool

Owner: Data Operations Team

## 1. Purpose

This Standard Operating Procedure (SOP) outlines the process for comparing column names and positions between two Excel files. The Excel Column Comparison Tool addresses the critical need to detect schema discrepancies that could affect data processing workflows, ETL operations, or analysis results. This procedure is designed for data engineers, analysts, and QA specialists who need to validate data structure consistency across different versions of Excel files.

## 2. Scope

This SOP covers the installation, configuration, and usage of the Excel Column Comparison Tool for identifying differences in column structure between Excel files. It applies to all Excel-based data validation processes within the organization but does not cover content comparison or cell-level data validation. This procedure complements existing data quality and ETL validation procedures.

## 3. Roles and Responsibilities

### Data Engineers
- Implement and maintain the comparison tool
- Execute comparisons during ETL development and updates
- Address identified structural issues in data pipelines

### Data Analysts
- Perform regular schema validation using the tool
- Document and report structural inconsistencies
- Verify data migration integrity

### QA Specialists
- Incorporate the tool into automated testing workflows
- Validate data structure before and after system updates
- Maintain comparison test suites

## 4. Prerequisites

### System Requirements
- Python 3.6 or higher installed
- Read access to Excel files being compared
- Write access to output location (if saving reports)

### Required Files
- `compare_excel.py` - Main script file
- `requirements.txt` - Dependencies file
- `README.md` - Basic instruction guide

### Required Python Packages
- openpyxl - For Excel file handling
- tabulate - For formatting comparison reports

## 5. Procedure

### 5.1 Installation

1. Ensure Python 3.6+ is installed on your system
   ```
   python --version
   ```

2. Download the tool files to a local directory
   - `compare_excel.py`
   - `requirements.txt`
   - `README.md`

3. Install required dependencies
   ```
   pip install -r requirements.txt
   ```

### 5.2 Basic Operation

1. Open a terminal or command prompt

2. Navigate to the directory containing the script
   ```
   cd path\to\script\directory
   ```

3. Run the comparison with two Excel files
   ```
   python compare_excel.py "PATH\TO\FIRST_FILE.xlsx" "PATH\TO\SECOND_FILE.xlsx"
   ```

4. Review the comparison results displayed in the console

5. (Optional) Save the results to a file by adding the output parameter
   ```
   python compare_excel.py "PATH\TO\FIRST_FILE.xlsx" "PATH\TO\SECOND_FILE.xlsx" -o "comparison_report.txt"
   ```

### 5.3 Interpretation of Results

The comparison report contains several key sections:

#### 5.3.1 Comparison Summary

Review the high-level metrics to assess the scale of differences:
- Total columns in each file
- Number of matching columns
- Number of columns with position mismatches
- Number of columns exclusive to each file

Example:
```
=== COMPARISON SUMMARY ===
File 1: sales_data_2024.xlsx
File 2: sales_data_2025.xlsx
Total columns in File 1: 15
Total columns in File 2: 17
Matching columns (same name and position): 12
Columns with position mismatches: 2
Columns only in File 1: 1
Columns only in File 2: 3
```

#### 5.3.2 Detailed Comparison

Examine the comprehensive table showing all columns with their positions and status:

```
=== DETAILED COMPARISON ===
+------------------+--------------------+--------------------+-----------------+
| Column Name      | Position in File 1 | Position in File 2 | Status          |
+==================+====================+====================+=================+
| Customer ID      | 0                  | 0                  | Match           |
+------------------+--------------------+--------------------+-----------------+
| Product Code     | 1                  | 1                  | Match           |
+------------------+--------------------+--------------------+-----------------+
| Sale Date        | 2                  | 4                  | Position Mismatch|
+------------------+--------------------+--------------------+-----------------+
| Old Field        | 3                  | N/A                | Only in File 1  |
+------------------+--------------------+--------------------+-----------------+
| New Field        | N/A                | 2                  | Only in File 2  |
+------------------+--------------------+--------------------+-----------------+
```

#### 5.3.3 Position Mismatches and Exclusive Columns

Pay special attention to:
- Position mismatches - Can cause data alignment issues in processing pipelines
- Exclusive columns - Identify added or removed data fields

### 5.4 Decision Making

1. For position mismatches:
   - Determine if column reordering is intentional
   - Update any position-dependent code in data pipelines
   - Document changes in data dictionary

2. For exclusive columns:
   - Verify if additions/removals are expected
   - Update dependent systems to accommodate changes
   - Consider data completeness implications

## 6. Error Handling & Troubleshooting

### 6.1 Common Errors

| Error Message | Possible Cause | Resolution |
|---------------|----------------|------------|
| `Error: File '...' does not exist.` | Incorrect file path | - Verify the file path is correct<br>- Ensure file names are spelled correctly<br>- Use absolute paths to avoid ambiguity |
| `Error reading file ...` | File format or access issues | - Ensure the file is a valid Excel file<br>- Check that the file isn't corrupted<br>- Verify you have read permissions<br>- Close the file if it's open in another application |
| `Error saving report to ...` | Write permission or path issues | - Check write permissions for the output directory<br>- Verify the output path exists<br>- Ensure the file isn't locked by another process |
| Missing module errors | Dependencies not installed | - Run `pip install -r requirements.txt`<br>- Verify Python environment is activated (if using venv) |

### 6.2 Support Resources

If issues persist after attempting the troubleshooting steps:
- Contact the Data Engineering team via Slack (#data-engineering)
- Create a ticket in JIRA under the DATA project
- Reference the tool's README.md for additional troubleshooting steps

## 7. Monitoring & Maintenance

### 7.1 Performance Monitoring

- **Memory Usage:**
  - The tool is designed to be memory-efficient by reading only header rows
  - Monitor system memory when comparing very large files (100+ columns)

- **Processing Time:**
  - Most comparisons should complete in seconds
  - Log execution time for baseline performance tracking

### 7.2 Regular Maintenance

1. **Dependency Updates:**
   - Check for openpyxl and tabulate updates quarterly
   - Update requirements.txt after testing with new versions

2. **Script Maintenance:**
   - Review script for improvements every 6 months
   - Version control changes through Git

### 7.3 Best Practices for Ongoing Use

- Include comparison reports in change management documentation
- Run comparisons before and after major data structure changes
- Integrate the tool into CI/CD pipelines for automated testing
- Archive comparison reports for audit purposes

## 8. References & Related Documents

### 8.1 Related Procedures
- Data Quality Assurance SOP
- ETL Validation Process
- Data Migration Checklist
- Schema Change Management Procedure

### 8.2 Technical References
- Python openpyxl Documentation: https://openpyxl.readthedocs.io/
- Internal Data Dictionary (Confluence)
- Corporate Data Governance Standards

### 8.3 Additional Resources
- Script GitHub Repository
- Example Comparison Reports
- Use Case Documentation

---

**Version History**

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | May 30, 2025 | Data Operations Team | Initial SOP creation |
