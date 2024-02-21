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











  WITH StatusFlow AS (
    SELECT
        *,
        ROW_NUMBER() OVER (PARTITION BY id ORDER BY s_no) AS row_num
    FROM
        your_table
)
SELECT DISTINCT
    sf1.id
FROM
    StatusFlow sf1
JOIN
    StatusFlow sf2 ON sf1.id = sf2.id AND sf1.row_num = sf2.row_num - 1
WHERE
    sf1.creator = 'yes' AND sf1.status = 'not seen'
    AND sf2.creator = 'yes' AND sf2.status = 'closed' AND sf2.agent IS NULL;





 MOD(ABS(FARM_FINGERPRINT(CAST(id AS STRING))) + ABS(FARM_FINGERPRINT(CAST(date_column AS STRING))), 3) AS split_group
  FROM 
