# sql12
patika.dev linkim: https://app.patika.dev/cmilakonur <br />

1- film tablosunda film uzunluğu length sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır? <br />

SELECT COUNT(*) FROM film <br />
WHERE length > (SELECT AVG(length) FROM film); <br />

2- film tablosunda en yüksek rental_rate değerine sahip kaç tane film vardır? <br />

SELECT COUNT((SELECT MAX(rental_rate) FROM film)) FROM film; <br />

3- film tablosunda en düşük rental_rate ve en düşün replacement_cost değerlerine sahip filmleri sıralayınız. <br />

SELECT title FROM film <br />
WHERE (rental_rate  = (SELECT MIN(rental_rate) FROM film)) AND (replacement_cost = (SELECT MIN(replacement_cost) FROM film)); <br />

4- payment tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız. <br />

SELECT customer.first_name, customer.last_name FROM customer <br />
JOIN payment On customer.customer_id = ANY <br />
(SELECT customer_id FROM payment <br />
GROUP BY customer_id  <br />
ORDER BY COUNT(customer_id) DESC <br />
LIMIT 5) <br />
LIMIT 5; <br />
