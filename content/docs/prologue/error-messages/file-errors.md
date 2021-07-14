---
title: "File Errors"
slug: "file-errors"
hidden: false
createdAt: "2019-07-01T13:59:11.463Z"
updatedAt: "2019-12-10T12:12:44.480Z"
---
The following error messages relate to file operations.

**ERROR_BATCH_FILE_DOES_NOT_EXIST_IN_PATH**
The request attempted a batch file operation, but the file was not found. The request was rejected. Corrective action: Set 'file' to the name of a file that was previously uploaded.

**ERROR_BATCH_FILE_MISSING_REQUIRED_FIELDS**
This record is missing one or more required fields. The request was rejected. Corrective action: Check all input parameters.

**ERROR_BATCH_FILE_NOT_FOUND**
The request attempted a batch file operation, but the request did not include the batch file. The request was rejected. Corrective action: Include the required batch file in the HTTP request.

**ERROR_BATCH_FILE_PARTNER_NOT_VALID**
The request attempted a batch file operation, but the partner was not found. The request was rejected. Corrective action: For 'partner', use the ID of a valid partner.

**ERROR_BATCH_FILE_TYPE_NOT_VALID**
The request attempted a batch file operation, but the file type could not be determined. The request was rejected. Corrective action: Set the 'type' field to 'batch_payout'.

**ERROR_BATCH_FILES_TOTAL_SIZE_EXCEEDED_MAX_SIZE**
The request attempted a batch file operation, but the file contained too many records, or there were too many batch files. The request was rejected. Corrective action: Send less files than MAX_SIZE and put less than MAX_SIZE number of records in each file.

**ERROR_CSV_FILE_NOT_VALID**
The request tried to upload a CSV file, but there was a problem with the format of the file. The request was rejected. Corrective action: Use a file that has correct CSV formatting.

**ERROR_GET_BATCH_FILE**
The request tried to perform an operation to fetch a file, but the file was not found. The request was rejected.

**ERROR_GET_BATCH_FILE_DETAILS**
The request tried to retrieve details of a batch file, but the batch file was not found. The request was rejected. Corrective action: Use the ID of a valid batch file.

**ERROR_MISSING_BATCH_FILE_REQUIRED_FIELDS**
The request attempted a batch file operation, but the file did not contain all fields required for the operation. The request was rejected. Corrective action: Send a CSV file that contains all required fields. The names of the missing fields appear at the end of the response code.

**ERROR_MISSING_BATCH_FILE_TYPE**
The request attempted a batch file operation, but the file type was not provided. The request was rejected. Corrective action: Set the 'type' field to 'batch_payout'.

**ERROR_NO_FILE_WAS_UPLOADED**
The request attempted a batch file operation, but no batch file was included in the request. The request was rejected. Corrective action: Upload the required type of batch file as part of the request.

**ERROR_PARSE_BATCH_FILE_RECORD**
This record could not be parsed. The request was rejected. Corrective action: Check all input parameters.

**ERROR_RETRIEVE_BATCH_FILE_DETAILS**
The request attempted an operation that requires the ID of a valid batch file, but the file was not found. The request was rejected. Corrective action: Use the ID of a valid batch file.

**MISSING_MANDATORY_HEADER**
The request tried to run a batch file operation, but one of the required header fields was missing. The name of the missing field appears at the end of the response code. The request was rejected. Corrective action: Include all required fields in the header of the batch file.