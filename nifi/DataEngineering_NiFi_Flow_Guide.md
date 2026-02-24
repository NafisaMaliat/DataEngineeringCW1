# Task 3 – Apache NiFi Dataflow Guide (Folder: DataEngineering)

Use this guide to build your NiFi flow and record your mandatory video demo.

## Target outcome

Pull data from MySQL (`techreads_db.techreads_books`), optionally transform fields, and write structured output to local directory as JSON/CSV.

## Create process group

1. Open NiFi UI.
2. Create a Process Group named **DataEngineering**.
3. Enter the group and add the processors below.

## Recommended processors and connections

1. **GenerateTableFetch**
   - Database Connection Pooling Service: `DBCPConnectionPool` (MySQL)
   - Table Name: `techreads_books`
   - Partitioning Column: `id`

2. **ExecuteSQLRecord**
   - Reads SQL from incoming FlowFile
   - Record Writer: `JsonRecordSetWriter` (or CSV writer)

3. **UpdateRecord** *(optional transformation)*
   - Clean/rename fields if needed

4. **PutFile**
   - Directory: e.g. `C:\Users\alvi9\MyWork\Data Engineering - Copy\nifi_output`
   - Conflict Resolution Strategy: `replace`

Connections:
- `GenerateTableFetch(success) -> ExecuteSQLRecord`
- `ExecuteSQLRecord(success) -> UpdateRecord`
- `UpdateRecord(success) -> PutFile`

## Controller services

Configure and enable:
- `DBCPConnectionPool` (MySQL JDBC URL, username, password)
- `JsonRecordSetWriter` (or CSVRecordSetWriter)
- `JsonTreeReader` if UpdateRecord is used

## Demo checklist (for your video)

1. Show DataEngineering group and configured processors.
2. Show controller services enabled.
3. Start flow and show generated output files in local directory.
4. Open one output file and confirm data fields.
5. Explain why NiFi automation is better than manual script running.

## Suggested demo narration points

- Why each processor is used
- How scheduling supports recurring ingestion
- How this fits end-to-end pipeline architecture
