## Co chcemy ustandaryzować?

### Komunikaty

Elektroniczna wymiana dokumentów opiera się o komunikaty. Na początek chcielibyśmy ustandaryzować sześć z nich:


STOCK ENQUIRY
  : Komunikat z żądaniem dostarczenia informacji o cenie (dla danego odbiorcy) i dostępności produktów

STOCK RESPONSE
  : Komunikat z informacją o dostępnych produktach i ich cenie dla żądającego

ORDER
  : komunikat wysyłany przez zamawiającego towar. Oprócz listy zamawianych produktów może zawierać dodatkowe informacje (dostawa/promocja z której korzysta zamawiający)

ORDER RESPONSE 
  : (komunikat nieobowiązkowy) - potwierdzenie przyjęcia zamówienia przez sprzedawcę. Na tym etapie sprzedawca może określić, 
    które produkty zostały skreślone z zamówienia (np. niedostępne w magazynie).

DESPATCH ADVICE 
  : (komunikat nieobowiązkowy) - informacja o wysyłce wraz ze szczegółową informacją o stopniu realizacji zamówienia (w stosunku do poprzedniego 
    komunikatu mogły nastąpić zmiany - na przykład wybrany tytuł nie został znaleziony w magazynie lub wszystkie egzemplarze są uszkodzone). 

INVOICE
  : informacja o wystawionej fakturze do zrealizowanego zamówienia.


### Droga wymiany komunikatów

Najbardziej uniwersalnym sposobem wymiany komunikatów jest E-mail. Każda firma musi mieć dwa adresy E-mail: jeden, na który mają być wysyłane komunikaty, drugi, na który będą odsyłane
informacje o błędach podczas przetwarzania komunikatów (ta skrzynka powinna być regularnie czytana przez wyznaczonego pracownika). 

Komunikat powinien być wklejony jako tekst w treści maila. Dopuszczalne jest też umieszczenie stopki, po linii skłającej się z przynajmniej dwóch myślników.

Przykład E-maila:

~~~

Date: Tue, 14 Nov 2017 16:25:42 +0000
From: edi <edi@publisher.com>
To: edi@company.com
Message-ID: <0102015fbb59c144-d95a7bd1-3473-46c6-9af2-a8f7e2b55336-000000@elibri.com.pl>
Subject: ORDER
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 7bit

<?xml version="1.0" encoding="UTF-8"?>
<Message>...</Message>

--
Tu znajduje się ignorowany przy przetwarzaniu komunikat
~~~

