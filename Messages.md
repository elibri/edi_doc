## Komunikaty


### STOCK ENQUIRY

Jest to żądanie otrzymania informacji o dostępnościach produktów wraz z cenami.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>STOCK_ENQUIRY</kind>
  <buyer>558710</buyer>
  <seller>112871</seller>
</message>
~~~

kind:
  : typ wiadomości, zawsze **STOCK_ENQUIRY**, *pole wymagane*

buyer:
  : kod strony zamawiającej w BookAddressDB, *pole wymagane*.

seller:
  : kod sprzedawcy w BookAddressDB, *pole wymagane*.


### STOCK RESPONSE

Jest to odpowiedź na żądanie informacji o dostępnych do sprzedaży produktach i ich cenach (opcjonalnie)

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>STOCK_RESPONSE</kind>
  <buyer>558710</buyer>
  <seller>112871</seller>
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
        <trade_net_price>25.20</trade_net_price>
      </trading_prices>
    </line_item>
  </line_items>
</message>
~~~

kind:
  : w tym komunikacie zawsze przyjmuje wartość **STOCK_RESPONSE**, *pole wymagane*

buyer:
  : kod strony zamawiającej w BookAddressDB, *pole wymagane*.

seller:
  : kod sprzedawcy w BookAddressDB, *pole wymagane*.

response_date:
  : data wygenerowania cennika, w formacie rrrr-mm-dd, *pole wymagane*

line_items:
  : zawiera zero lub więcej elementów `<line_item>`. Jeśli sprzedający nie współpracuje z kontrahentem, albo odmawia wygenerowania cennika, to powinien
    wygenerować pusty tag `<line_items/>`

    line_item: 
      : linia zamówienia

        ean:
          : EAN produktu, *pole wymagane*

        description:
          : nazwa produktu

        stock_quantity:
          : przybliżona ilość dostępna od ręki do sprzedaży, *pole wymagane*

        expected_ship_date:
          : data pierwszego dnia (w formacie rrrr-mm-dd), w którym będą realizowane zamówienia na ten produkt. 
            W ten sposób można zasygnalizować, kiedy książka będzie dostępna do sprzedaży. 
            Gdy jest podana ta data, to w polu `<stock_quantity>` proszę podawać 0.

        consumer_on_sale_date:
          : w tym polu można podać datę, od kiedy książka może być sprzedawana klientom końcowym, w formacie rrrr-mm-dd.

        retail_price_including_tax:
          : w tym polu można podać cenę detaliczną produktu z podatkiem VAT.

        tax:
          : stawka podatku VAT, w postaci liczby (bez znaku %)

        trade_prices:
          : informacja o cenach sprzedaży produktu dla kontrahenta określonego w tagu `<buyer>`. Cena może zostać powtórzona kilka razy z różną minimalną ilością zakupu produktu.

            trade_price: 
              : block informujący o cenie sprzedaży 

                trade_net_price:
                  : cena netto zakupu produktu

                minimal_amount:
                  : minimalna ilość, którą trzeba zamówić. Brak tego taga oznacza, że minimalna ilość, którą trzeba zamówić to 1 szt./egz.


### ORDER

Zamówienie na produkty. Zamówienie jest realizowane tylko raz, to znaczy, że produkty niedostępne w momencie realizacji zamówienia nie będą później dosyłane. 
Jeśli zamawiane produkty staną się dostępne w późniejszym terminie, muszą zostać ponownie zamówione.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>ORDER</kind>
  <buyer_number>SK/18777/2017</buyer_number>
  <buyer>558710</buyer>
  <seller>112871</seller>
  <delivery>558728</delivery>
  <order_date>2017-11-19</order_date>
  <line_items>
    <line_item>
      <quantity>2</quantity>
      <ean>9788388722639</ean>
      <description>Pamięć miłości</description>
    </line_item>
    <line_item>
      <quantity>3</quantity>
      <ean>9788388722684</ean>
      <description>Dziedzictwo ziemi</description>
    </line_item>
  </line_items>
</message>
~~~

kind:
  : w komunikacie zamówienia zawsze przyjmuje wartość **ORDER**, *pole wymagane*

buyer_number:
  : numer zamówienia w systemie zamawiającego, *pole wymagane*.

buyer:
  : kod zamawiającego w BookAddressDB, *pole wymagane*.

seller:
  : kod sprzedawcy w BookAddressDB, *pole wymagane*.

delivery:
  : kod miejsca dostawy w BookAddressDB. W przypadku braku tego pola przyjmowana jest wartość z pola buyer

order_date:
  : data złożenia zamówienia, w formacie rrrr-mm-dd

line_items:
  : linie zamówienia.

    line_item:
      : linia zamówienia

        quantity:
          : ilość zamawianego produktu, *pole wymagane*.

        ean:
          : EAN zamawianiego produktu, *pole wymagane*.

        description:
          : nazwa towaru

### ORDER RESPONSE

Jest to odpowiedż na zamówienie (nie można odpowiadać jednocześnie na kilka zamówień w jednym komunikacie *ORDER RESPONSE*). W odpowiedzi powinna znaleźć się informacja o pozycjach,
które sprzedawca ma zamiar zrealizować (o części z góry wiadomo, że nie są dostępne). Jeśli sprzedawca odmawia realizacji zamówienia, to powinien wysłać komunikat tylko z nagłówkiem,
bez żadnego produktu.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>ORDER_RESPONSE</kind>
  <seller_number>11/2017</seller_number>
  <buyer_number>SK/18777/2017</buyer_number>
  <buyer>558710</buyer>
  <seller>112871</seller>
  <delivery>558728</delivery>
  <line_items>
    <line_item>
      <quantity>1</quantity>
      <ean>9788388722639</ean>
      <net_price>19.93</net_price>
      <net_amount>19.93</net_amount>
      <tax_rate>5</tax_rate>
      <tax_amount>1.00</tax_amount>
      <description>Pamięć miłości</description>
    </line_item>
    <line_item>
      <quantity>3</quantity>
      <ean>9788388722684</ean>
      <net_price>25.2</net_price>
      <net_amount>75.6</net_amount>
      <tax_rate>5</tax_rate>
      <tax_amount>3.78</tax_amount>
      <description>Dziedzictwo ziemi</description>
    </line_item>
  </line_items>
</message>
~~~

Są tu powtórzone pola z komunikatu *ORDER*, z wyjątkiem:

kind:
  : rodzaj wiadomości, przyjmuje wartość **ORDER_RESPONSE**

seller_number:
  : jest to numer zamówienia w systemie sprzedającego, *pole wymagane*

line_items:
  : line_item:
      : Pola związane z ceną zakupu nie są obowiązkowe, ale bardzo polecamy podawanie tych wartości

        quantity: 
          : musi być większa od zera. Jeśli wybrana pozycja nie może być zrealizowana, powinna zostać usunięta z dokumentu.

        net_price:
          : cena sprzedaży jednostkowa netto.

        net_amount:
          : suma netto

        tax_rate:
          : stawka VAT

        tax_amount:
          : wartość VAT


### DESPATCH ADVICE

Jest to informacja o wysyłce produktów.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>DESPATCH_ADVICE</kind>
  <seller_number>11/2017</seller_number>
  <buyer_number>SK/18777/2017</buyer_number>
  <buyer>558710</buyer>
  <seller>112871</seller>
  <delivery>558728</delivery>
  <line_items>
    <line_item>
      <quantity>3</quantity>
      <ean>9788388722684</ean>
      <net_price>25.2</net_price>
      <net_amount>75.6</net_amount>
      <tax_rate>5</tax_rate>
      <tax_amount>3.78</tax_amount>
      <description>Dziedzictwo ziemi</description>
    </line_item>
  </line_items>
</message>

~~~

Są tu powtórzone pola z komunikatu *ORDER_RESPONSE*, z wyjątkiem:

kind:
  : rodzaj wiadomości, przyjmuje wartość **DESPATCH_ADVICE**


### INVOICE

Jest to faktura wystawiona za towar. Do jednego zamówienia może zostać wystawiona jedna faktura.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>INVOICE</kind>
  <invoice_number>29991/S/2017</invoice_number>
  <seller_number>11/2017</seller_number>
  <buyer_number>SK/18777/2017</buyer_number>
  <buyer>558710</buyer>
  <seller>112871</seller>
  <delivery>558728</delivery>
  <invoice_date>2017-11-20</invoice_date>
  <sales_date>2017-11-20</sales_date>
  <payment_due_date>2017-12-03</payment_due_date>
  <seller_name>Wydawnictwo Dobre książki z o. o.</seller_name>
  <seller_address>ul Kolejowa 9/11</seller_address>
  <seller_city>Warszawa</seller_city>
  <seller_post_code>01-217</seller_post_code>
  <seller_tax_id>9744287572</seller_tax_id>
  <buyer_name>Księgarnia Superksiążki sp. z o. o.</buyer_name>
  <buyer_address>Al. Niepodległości 1</buyer_address>
  <buyer_city>Warszawa</buyer_city>
  <buyer_post_code>02-653</buyer_post_code>
  <buyer_tax_id>1270286596</buyer_tax_id>
  <delivery_detail_name>Superksiążki - Magazyn</delivery_detail_name>
  <delivery_detail_address>ul. Czarna 1</delivery_detail_address>
  <delivery_detail_city>Warszawa</delivery_detail_city>
  <delivery_detail_post_code>02-997</delivery_detail_post_code>
  <pdf>--obraz faktury pdf zakodowany base64--</pdf>
  <line_items>
    <line_item>
      <quantity>3</quantity>
      <net_price>25.2</net_price>
      <net_amount>75.6</net_amount>
      <tax_rate>5</tax_rate>
      <tax_amount>3.78</tax_amount>
      <ean>9788388722684</ean>
      <description>Dziedzictwo ziemi</description>
    </line_item>
  </line_items>
  <summary>
    <total_lines>1</total_lines>
    <net_amount>75.6</net_amount>
    <tax_amount>3.78</tax_amount>
    <gross_amount>79.38</gross_amount>
    <tax_rate_summaries>
      <tax_rate_summary>
        <tax_rate>5</tax_rate>
        <net_amount>75.6</net_amount>
        <tax_amount>3.78</tax_amount>
        <gross_amount>79.38</gross_amount>
      </tax_rate_summary>
    </tax_rate_summaries>
  </summary>
</message>
~~~

kind:
  : typ wiadomości, zawsze **INVOICE**, *pole wymagane*

invoice_number:
  : numer wystawionej faktury, *pole wymagane*

buyer_number:
  : numer zamówienia w systemie zamawiającego, *pole wymagane*.

seller_number:
  : jest to numer zamówienia w systemie sprzedającego, *pole wymagane*

buyer:
  : kod zamawiającego w BookAddressDB, *pole wymagane*.

seller:
  : kod sprzedawcy w BookAddressDB, *pole wymagane*.

delivery:
  : kod miejsca dostawy w BookAddressDB. W przypadku braku tego pola przyjmowana jest wartość z pola buyer

invoice_date:
  : data wystawienia faktury, w formacie rrrr-mm-dd, *pole wymagane*

sales_date:
  : data sprzedaży, w formacie rrrr-mm-dd, *pole wymagane*

payment_due_date:
  : termin płatności, w formacie rrrr-mm-dd, *pole wymagane*

seller_name:
  : nazwa sprzedawcy, *pole wymagane*

seller_address:
  : adres sprzedającego - ulica, *pole wymagane*

seller_city:
  : adres sprzedającego - miasto, *pole wymagane*

seller_post_code:
  : adres sprzedającego - kod pocztowy, *pole wymagane*

seller_tax_id:
  : NIP sprzedającego, *pole wymagane*

buyer_name:
  : nazwa kupującego, *pole wymagane*

buyer_address:
  : adres kupującego - ulica, *pole wymagane*

buyer_city:
  : adres kupującego - miasto, *pole wymagane*

buyer_post_code:
  : adres kupującego, - kod pocztowy, *pole wymagane*

buyer_tax_id:
  : NIP kupującego, *pole wymagane*

delivery_detail_name:
  : nazwa miejsca dostarczenia towaru, *pole wymagane jeśli obecna jest wartość delivery*

delivery_detail_address:
  : adres dostarczenia towaru - ulica, *pole wymagane jeśli obecna jest wartość delivery*

delivery_detail_city:
  : adres dostarczenia towaru - miasto, *pole wymagane jeśli obecna jest wartość delivery*

delivery_detail_post_code:
  : adres dostarczenia towaru - kod pocztowy, *pole wymagane jeśli obecna jest wartość delivery*

pdf:
  : obraz faktury pdf zakodowany w base64

line_items:
  : linie fakturty

    line_item:
      : linia faktury

        quantity:
          : ilość produktu, *pole wymagane*.

        ean:
          : EAN produktu, *pole wymagane*.

        net_price:
          : cena sprzedaży jednostkowa netto, *pole wymagane*

        net_amount:
          : suma netto, *pole wymagane*

        tax_rate:
          : stawka VAT, *pole wymagane*

        tax_amount:
          : wartość VAT, *pole wymagane*

        description:
          : nazwa towaru

summary:
  : podsumowanie dokumentu

    total_lines:
      : liczba pozycji na fakturze, *pole wymagane*

    net_amount:
      : wartość netto faktury, *pole wymagane*

    tax_amount:
      : wartość VAT, *pole wymagane*

    gross_amount:
      : wartość brutto faktury, *pole wymagane*

    tax_rate_summaries:
      : podsumowanie faktury pogrupowane według stawek VAT, *pole wymagane*

        tax_rate_summary:
          : podsumowanie dla jednej stawki podatku VAT. Musi wystąpić przynajmniej raz.

            tax_rate:
              : stawka VAT, *pole wymagane*

            net_amount:
              : wartość netto, *pole wymagane*

            tax_amount:
              : wartość VAT, *pole wymagane*

            gross_amount:
              : wartość brutto dla określonej w polu tax_rate stawki VAT, *pole wymagane*


