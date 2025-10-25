 

-- Count records
SELECT COUNT(*) FROM border_traffic;

-- Check unique control points and directions
SELECT DISTINCT control_point FROM border_traffic;
SELECT DISTINCT direction FROM border_traffic;

-- Check date range
SELECT MIN(date), MAX(date) FROM border_traffic;

--Total Pessengers Traffic
SELECT SUM(total) AS total_passengers FROM border_traffic;

--Arrival vs Departure
SELECT direction, SUM(total) AS total_passengers
FROM border_traffic
GROUP BY direction
ORDER BY total_passengers DESC;

--Total by control points
SELECT control_point, SUM(total) AS total_passengers
FROM border_traffic
GROUP BY control_point
ORDER BY total_passengers DESC;

--Total passengers by month
SELECT
    DATE_TRUNC('month', date) AS month,
    SUM(total) AS total_passengers
FROM border_traffic
GROUP BY month
ORDER BY month;

--Busiest control points (overall)
SELECT
    control_point,
    SUM(total) AS total_traffic
FROM border_traffic
GROUP BY control_point
ORDER BY total_traffic DESC
LIMIT 10;


--Arrival vs Departure Traffic
SELECT
    direction,
    SUM(total) AS total_passengers,
    ROUND(SUM(total) * 100.0 / (SELECT SUM(total) FROM border_traffic), 2) AS percentage
FROM border_traffic
GROUP BY direction;

--Traffic by visitor type
SELECT
    'Hong Kong Residents' AS visitor_type,
    SUM(hk_residents) AS total
FROM border_traffic
UNION ALL
SELECT
    'Mainland Visitors', SUM(mainland_visitors)
FROM border_traffic
UNION ALL
SELECT
    'Other Visitors', SUM(other_visitors)
FROM border_traffic;

--Top 5 control points for arrivals vs departures
SELECT
    direction,
    control_point,
    SUM(total) AS total_passengers
FROM border_traffic
GROUP BY direction, control_point
ORDER BY direction, total_passengers DESC;

--Monthly growth rate
WITH monthly AS (
    SELECT
        DATE_TRUNC('month', date) AS month,
        SUM(total) AS total_passengers
    FROM border_traffic
    GROUP BY month
)
SELECT
    month,
    total_passengers,
    ROUND((total_passengers - LAG(total_passengers) OVER (ORDER BY month)) * 100.0 /
           LAG(total_passengers) OVER (ORDER BY month), 2) AS growth_rate_percent
FROM monthly;

--Average daily traffic per control point
SELECT
    control_point,
    ROUND(AVG(total)) AS avg_daily_passengers
FROM border_traffic
GROUP BY control_point
ORDER BY avg_daily_passengers DESC;

--Seasonal pattern detection (weekday analysis)
SELECT
    TO_CHAR(date, 'Day') AS weekday,
    ROUND(AVG(total)) AS avg_passengers
FROM border_traffic
GROUP BY weekday
ORDER BY avg_passengers DESC;


--Year on Year traffic comparison
SELECT
    DATE_PART('year', date) AS year,
    SUM(total) AS total_passengers,
    ROUND(
        (SUM(total) - LAG(SUM(total)) OVER (ORDER BY DATE_PART('year', date))) * 100.0 /
         LAG(SUM(total)) OVER (ORDER BY DATE_PART('year', date)), 2
    ) AS yoy_growth_percent
FROM border_traffic
GROUP BY year
ORDER BY year;


--KPI's
SELECT
    DATE_TRUNC('month', date) AS month,
    SUM(hk_residents) AS total_hk_residents,
    SUM(mainland_visitors) AS total_mainland_visitors,
    SUM(other_visitors) AS total_other_visitors,
    SUM(total) AS total_passengers,
    ROUND(SUM(hk_residents) * 100.0 / SUM(total), 2) AS hk_share,
    ROUND(SUM(mainland_visitors) * 100.0 / SUM(total), 2) AS mainland_share,
    ROUND(SUM(other_visitors) * 100.0 / SUM(total), 2) AS other_share
FROM border_traffic
GROUP BY month
ORDER BY month;




