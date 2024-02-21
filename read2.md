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
