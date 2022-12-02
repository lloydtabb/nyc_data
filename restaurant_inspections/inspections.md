# NYC Restaurant Inspections

NYC public data.  Data comes from here:

  https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j

<!-- malloy-source  
  title="Inspections"
  model="inspections.malloy"
  source="inspections"
  description="Explore Restaurant Inspections"
-->

<!-- malloy-query
  name="Violation Dashboard"
  description="Change the filter " 
  model="inspections.malloy"
  renderer="dashboard"
-->
```malloy
query: violation_dashboard is inspections -> {
  where: DBA = 'BROOKLYN WAFFLE HOUSE'
  group_by: 
    `VIOLATION CODE`
    `VIOLATION DESCRIPTION`
  aggregate: 
    inspection_count
    restaurant_count
  nest: 
    by_location
    `Violation Dates` is {
      group_by: `INSPECTION DATE_day` is `INSPECTION DATE`.day
    }
  limit: 20
}
```