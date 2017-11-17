## Komunikaty


### STOCK ENQUIRY

Jest to żądanie otrzymania informacji o dostępnościach produktów wraz z cenami.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>STOCK_ENQUIRY</kind>
  <buyer>SUPERSKLEP</buyer>
  <seller>WYDAWNICTWO-DOBRE-KSIAZKI</seller>
</message>
~~~

kind:
  : typ wiadomości, zawsze **STOCK_ENQUIRY**, *pole wymagane*
  
buyer:
  : kod strony zamawiającej, *pole wymagane*.

seller:
  : kod sprzedawcy, *pole wymagane*.


### STOCK RESPONSE

Jest to odpowiedź na żądanie informacji o dostępnych do sprzedaży produktach i ich cenach (opcjonalnie)
 
~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>STOCK_RESPONSE</kind>
  <buyer>SUPERSKLEP</buyer>
  <seller>WYDAWNICTWO-DOBRE-KSIAZKI</seller>
  <response_date>2017-11-19</response_date>
  <line_items>
    <line_item>
      <ean>9788388722639</ean>
      <description>Pamięć miłości</description>
      <stock_quantity>12</stock_quantity>
      <retail_price_including_tax>29.90</retail_price_including_tax>
      <tax>5</tax>
      <trading_prices>
        <trade_price>
          <trade_price_excluding_tax>19.93</trade_price_excluding_tax>
          <minimal_amount>1</minimal_amount>
        </trade_price>
        <trade_price>
          <trade_price_excluding_tax>17.09</trade_price_excluding_tax>
          <minimal_amount>10</minimal_amount>
        </trade_price>
      </trading_prices>
    </line_item>
    <line_item>
      <ean>9788388722684</ean>
      <description>Dziedzictwo ziemi</description>
      <stock_quantity>50</stock_quantity>
      <expected_ship_date>2017-12-01</expected_ship_date>
      <consumer_on_sale_date>2017-12-05</consumer_on_sale_date>
      <retail_price_including_tax>39.90</retail_price_including_tax>
      <tax>5</tax>
      <trading_prices>
        <trade_price_excluding_tax>26.60</trade_price_excluding_tax>
      </trading_prices>
    </line_item>
  </line_items>
</message>
~~~

kind:
  : w tym komunikacie zawsze przyjmuje wartość **STOCK_RESPONSE**, *pole wymagane*

buyer:
  : kod strony zamawiającej, *pole wymagane*.

seller:
  : kod sprzedawcy, *pole wymagane*.

response_date:
  : data wygenerowania cennika, w formacie rrrr-mm-dd, *pole wymagane*

line_items:
  : zawiera zero lub więcej elementów `<line_item>`. Jeśli sprzedający nie współpracuje z kontrahentem, albo odmawia wygenerowania cennika, to powinien
    wygenerować pusty tag `<line_items/>`

line_item.ean:
  : EAN produktu, *pole wymagane*

line_item.description:
  : nazwa produktu

line_item.stock_quantity:
  : przybliżona ilość dostępna od ręki do sprzedaży, *pole wymagane*

line_item.expected_ship_date:
  : data pierwszego dnia (w formacie rrrr-mm-dd), w którym będą realizowane zamówienia na ten produkt. W ten sposób można zasygnalizować, kiedy książka będzie dostępna do sprzedaży. 
    Gdy jest podana ta data, to w polu `<stock_quantity>` proszę podawać 0.

line_item.consumer_on_sale_date:
  : w tym polu można podać datę, od kiedy książka może być sprzedawana klientom końcowym, w formacie rrrr-mm-dd.

line_item.retail_price_including_tax:
  : w tym polu można podać cenę detaliczną produktu z podatkiem VAT.

line_item.tax:
  : stawka podatku VAT, w postaci liczby (bez znaku %)

line_item.trade_prices:
  : informacja o cenach sprzedaży produktu dla kontrahenta określonego w tagu `<buyer>`. Cena może zostać powtórzona kilka razy z różną minimalną ilością zakupu produktu.

trade_prices.trade_price_excluding_tax:
  : cena netto zakupu produktu

trade_prices.minimal_amount:
  : minimalna ilość, którą trzeba zamówić. Brak tego taga oznacza, że minimalna ilość, którą trzeba zamówić to 1 szt./egz.


### ORDER

Zamówienie na produkty. Zamówienie jest realizowane tylko raz, to znaczy, że produkty niedostępne w momencie realizacji zamówienia nie będą później dosyłane. 
Jeśli zamawiane produkty staną się dostępne w późniejszym terminie, muszą zostać ponownie zamówione.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>ORDER</kind>
  <buyer_number>SK/18777/2017</buyer_number>
  <buyer>SUPERSKLEP</buyer>
  <seller>WYDAWNICTWO-DOBRE-KSIAZKI</seller>
  <delivery>SUPERSKLEP-M1</delivery>
  <order_date>2017-11-19</order_date>
  <line_items>
    <line_item>
      <quantity>2</quantity>
      <ean>9788388722639</ean>
      <buyer_code>SK101</buyer_code>
      <description>Pamięć miłości</description>
      <position>1</position>
    </line_item>
    <line_item>
      <quantity>3</quantity>
      <ean>9788388722684</ean>
      <buyer_code>SK102</buyer_code>
      <description>Dziedzictwo ziemi</description>
      <position>2</position>
    </line_item>
  </line_items>
</message>
~~~

kind:
  : w komunikacie zamówienia zawsze przyjmuje wartość **ORDER**, *pole wymagane*

buyer_number:
  : numer zamówienia w systemie zamawiającego, *pole wymagane*.

buyer:
  : kod zamawiającego, *pole wymagane*.

seller:
  : kod sprzedawcy, *pole wymagane*.

delivery:
  : kod miejsca dostawy. W przypadku braku tego pola przyjmowana jest wartość z pola buyer

order_date:
  : data złożenia zamówienia, w formacie rrrr-mm-dd

line_items:
  : linie zamówienia. Każda linia jest zawarta w tagu `<line_item>`

line_item.quantity:
  : ilość zamawianego produktu, *pole wymagane*.

line_item.ean:
  : EAN zamawianiego produktu, *pole wymagane*.

line_item.buyer_code:
  : kod zamawiającego

line_item.description:
  : nazwa towaru

line_item.position: 
  : numer linii, *pole wymagane*.

### ORDER RESPONSE

### DESPATCH ADVICE

### INVOICE

