# FPSX Workload Template

This is a template repository for creating Scale Test workload projects. This template provides a standardized folder structure and sample files to help you quickly set up performance testing workloads using JMeter.

## 📁 Repository Structure

**⚠️ IMPORTANT: This folder structure MUST be maintained for proper Scale Test functionality.**

```
fpsx-workload-template/
├── data-files/           # CSV data files for test parameterization
│   ├── sample-data-1.csv
│   └── sample-data-2.csv
├── test-plans/           # JMeter test plan files (.jmx)
│   ├── sample-script-1.jmx
│   └── sample-script-2.jmx
├── user-files/           # User credential files
│   └── sample-users-1.csv
└── workload-metadata/    # Workload configuration metadata
    └── sample-metadata.json
```

## 📋 Folder Descriptions

### `data-files/`
Contains CSV files with test data that can be used to parameterize your JMeter tests. These files typically include:
- Test data for HTTP requests
- Configuration parameters
- Input values for different test scenarios

**Example format:**
```csv
column1,column2,column3
value1,value2,value3
value4,value5,value6
```

### `test-plans/`
Contains JMeter test plan files (`.jmx` format) that define your performance test scenarios. These files:
- Define the test structure and logic
- Reference data files and user files through JMeter variables
- Can be configured to use relative paths to other folders in this template

### `user-files/`
Contains CSV files with user credentials and authentication data. These files typically include:
- Usernames and passwords

**Example format:**
```csv
username,password
user1,password1
user2,password2
```

### `workload-metadata/`
Contains JSON configuration files that define how the workload components work together. The metadata file specifies:
- JMeter version requirements
- Task definitions linking scripts to data files
- File associations and dependencies

**Example structure:**
```json
{
    "jmeter_version": "5.6.3",
    "tasks": [
        {
            "task_name": "sample-task-1",
            "script_name": "sample-script-1.jmx",
            "users_file": "sample-users-1.csv",
            "data_files": {
                "sample-data-1": "sample-data-1.csv"
            }
        }
    ]
}
```

## 🚀 Getting Started

1. **Clone this template repository**
   - This is a template repository. You can use this repository to create your own.

2. **Customize the workload metadata**
   - Edit `workload-metadata/sample-metadata.json`
   - Define your tasks with appropriate file associations

3. **Replace sample files with your content**
   - Add your JMeter test plans to `test-plans/`
   - Add your test data to `data-files/`
   - Add your user credentials to `user-files/`

4. **Update file references**
   - Ensure your JMeter scripts reference the correct data and user files
   - Use relative paths as shown in the sample files
   - Update the metadata.json to match your new file names

## 📝 File Naming Conventions

- **Test Plans**: Use descriptive names ending with `.jmx` (e.g., `login-performance-test.jmx`)
- **Data Files**: Use descriptive names ending with `.csv` (e.g., `product-catalog-data.csv`)
- **User Files**: Use descriptive names ending with `.csv` (e.g., `test-users.csv`)
- **Metadata**: Keep as `sample-metadata.json` or use descriptive names ending with `.json`

## 🔧 JMeter Configuration

The sample JMeter scripts in this template are configured to:
- Accept external parameters for file locations
- Work with the Scale Test execution environment

Example JMeter variable configuration:
```xml
<elementProp name="USERS_FILE" elementType="Argument">
    <stringProp name="Argument.name">USERS_FILE</stringProp>
    <stringProp name="Argument.value">${__P(username_file,../user-files/sample-users-1.csv)}</stringProp>
</elementProp>
```

## ⚠️ Important Notes

1. **Folder Structure**: Do NOT modify the folder structure. Scale Test functionality depends on this specific layout.

2. **File Paths**:
    - User files will be sent to Jmeter script as `-Jusername_file=../user-files/sample-users-1.csv`
    - Other data files will use the key mentioned in the metadata json eg: `-Jsample-data-1=../data-files/sample-data-1.csv`

3. **File Extensions**: 
   - JMeter files must use `.jmx` extension
   - Data files should use `.csv` extension
   - Metadata files should use `.json` extension

4. **Version Compatibility**: Ensure your JMeter version matches the version specified in the metadata file.

---
**Compatible JMeter Version**: 5.6.3