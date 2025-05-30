# 0.2.0 - Add: Bulk csv upload for RN
- registered nurse patch endpoint /api/rn-reporting-csv accepts sample csv file from /sample-data/nurse_attendance_data.csv
- csv to json conversion in mule app in process-layer.xml
- sends the result to the /api/RegisteredNurseAttendance/{id} endpoint
- added setVar to all flows for easy usage
- added more bruno tests
- all requests currently pointing at localhost, need to update to https://dohac-apis.fly.dev in next edit
- not yet deployed to cloudhub

# 0.1.1 - Add: README.md
- added README.md
- changed pom.xml version to 1.0.0-SNAPSHOT since these are demo assets
# 0.1.0 - Add: initial commit
- 3 endpoints mocked in Mule to dohac-apis.fly.dev
