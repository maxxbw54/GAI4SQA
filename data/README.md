# [Stack Overflow Data Explorer](https://data.stackexchange.com/stackoverflow/query/new)

```
SELECT pq.Id, pq.PostTypeId, pq.Title, pq.Body, pq.AcceptedAnswerId, pa.Body as AcceptedAnswer 
FROM posts pq JOIN posts pa
ON pq.AcceptedAnswerId = pa.Id
WHERE
pq.PostTypeId = 1 AND -- Questions
pq.CreationDate BETWEEN '01-JAN-2022' AND '31-DEC-2022' AND -- Time
pq.AcceptedAnswerId IS NOT NULL AND -- Have accepted answer
pq.Id NOT IN (SELECT PostId FROM PostLinks WHERE LinkTypeId = 3) AND -- No duplicate question
pq.Id NOT IN (SELECT RelatedPostId FROM PostLinks WHERE LinkTypeId = 3) AND -- No duplicate question
pq.Tags LIKE '%<java>%' AND
pq.Body NOT LIKE '%<img src="%">%' AND 
pq.Score > 5
```