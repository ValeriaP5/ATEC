SELECT activation_date_utc, MAX(activation_date_utc) AS highest_value
FROM tbl_activation_no_filter
WHERE activation_type = 'GSM_Angaza'
GROUP BY activation_date_utc;
