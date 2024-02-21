WITH RankedCases AS (
  SELECT
    ID,
    status,
    reason,
    UpdatedTime,
    region,
    channel,
    ROW_NUMBER() OVER (PARTITION BY ID ORDER BY UpdatedTime DESC) AS RowNum
  FROM
    YourTableName
)

SELECT
  ID,
  status,
  reason,
  UpdatedTime,
  region,
  channel
FROM
  RankedCases
WHERE
  RowNum = 1;




 MOD(ABS(FARM_FINGERPRINT(CAST(id AS STRING))) + ABS(FARM_FINGERPRINT(CAST(date_column AS STRING))), 3) AS split_group
  FROM 
