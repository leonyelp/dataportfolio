# dataportfolio
My kind of exploratory teritory
select
  category,
  round(sum(case when extract(year from order_date)=2021 then after_discount else 0 end),2) as nilai_transaksi_2021,
  round(sum(case when extract(year from order_date)=2022 then after_discount else 0 end),2) as nilai_transaksi_2022,
  round (
      sum (case when extract(year from order_date)= 2022 then after_discount else 0 end) -
      sum (case when extract(year from order_date)= 2021 then after_discount else 0 end) ,2)
      as margin

from `finpro_data.order_details`
left join `finpro_data.sku_detail` on `finpro_data.order_details`.sku_id = `finpro_data.sku_detail`.id
where extract(year from order_date) in (2021,2022)
and is_valid =1
group by 1
order by margin asc
