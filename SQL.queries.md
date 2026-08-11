**#How many users reached the product page?**



SELECT COUNT(\*) AS total\_sessions FROM sessions;

SELECT variant, COUNT(\*) AS sessions

FROM sessions

GROUP BY variant;



**#Add-to-cart rate by variant**



SELECT variant, COUNT(\*) AS sessions,

SUM(added\_to\_cart) AS add\_to\_carts, ROUND(100.0 \* SUM(added\_to\_cart) / COUNT(\*), 2) AS atc\_rate\_pct

FROM sessions

GROUP BY variant;



**#Purchase conversion rate by variant**



SELECT variant,COUNT(\*) AS sessions,SUM(purchased) AS purchases,

ROUND(100.0 \* SUM(purchased) / COUNT(\*), 2) AS purchase\_conv\_rate\_pct

FROM sessions

GROUP BY variant;



**#Revenue per visitor by variant**



SELECT variant,COUNT(\*) AS sessions,SUM(revenue) AS total\_revenue,

ROUND(SUM(revenue) \* 1.0 / COUNT(\*), 2) AS revenue\_per\_visitor

FROM sessions

GROUP BY variant;  



**#Which device responds best?**



SELECT device, 

ROUND(100.0 \* SUM(CASE WHEN variant='A' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='A' THEN 1 ELSE 0 END), 2) AS conv\_rate\_A\_pct,

ROUND(100.0 \* SUM(CASE WHEN variant='B' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='B' THEN 1 ELSE 0 END), 2) AS conv\_rate\_B\_pct,

ROUND(

(100.0 \* SUM(CASE WHEN variant='B' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='B' THEN 1 ELSE 0 END))-(100.0 \* SUM(CASE WHEN variant='A' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='A' THEN 1 ELSE 0 END))

, 2) AS pct\_point\_lift

FROM sessions

GROUP BY device

ORDER BY pct\_point\_lift DESC;



**Which ProductCategory responds best?**



SELECT product\_category,

ROUND(100.0 \* SUM(CASE WHEN variant='A' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='A' THEN 1 ELSE 0 END), 2) AS conv\_rate\_A\_pct,

ROUND(100.0 \* SUM(CASE WHEN variant='B' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='B' THEN 1 ELSE 0 END), 2) AS conv\_rate\_B\_pct,

ROUND(

(100.0 \* SUM(CASE WHEN variant='B' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='B' THEN 1 ELSE 0 END))-(100.0 \* SUM(CASE WHEN variant='A' THEN purchased ELSE 0 END)

/ SUM(CASE WHEN variant='A' THEN 1 ELSE 0 END))

, 2) AS pct\_point\_lift

FROM sessions

GROUP BY product\_category

ORDER BY pct\_point\_lift DESC;



**# Raw counts needed for the significance test**



SELECT variant,SUM(purchased) AS converted,

COUNT(\*)-SUM(purchased) AS not\_converted,

COUNT(\*) AS total

FROM sessions

GROUP BY variant;

This produces the 2x2 contingency table (converted/not-converted\[by variant]) that feeds

directly into the statistical test





