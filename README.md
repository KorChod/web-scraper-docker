# Opis projektu

Frameworki które użyłem w projekcie to Django i Django REST Framework.

Do obsługi zadań asynchronicznych wykorzystałem Celery z brokerem RabbitMQ.

Aplikacja została zdokeryzowana przy użyciu Dockera aby ułatwić zarządzanie bibliotekami i zależnościami w projekcie.

Do oddzielenia tekstu i zdjęć oraz usunięcia tagów HTML ze strony docelowej użyłem biblioteki BeautifulSoup.

Stworzyłem 3 modele:
- Webpage: reprezentujący stronę (posiada pola url i tekst);
- Image: reprezentujący zdjęcia powiązane ze stroną;
- AsyncResult: przetrzymujący obecny stan naszego zadania asynchronicznego jak pobranie tekstu lub zdjęć.

Zdefiniowałem 5 punktów wejścia dla api:
- '/api/scrape/text/': obsługujący metodę POST, rozpoczyna procedurę pobrania tekstu ze strony. W zapytaniu należy określić parametr "url";
- '/api/scrape/images/': obsługujący metodę POST, rozpoczyna procedurę pobrania zdjęć ze strony. W zapytaniu należy określić parametr "url";
- '/api/webpages/': obsługujący metodę GET, wyświetla dane z wcześniej pobranych stron. Dzięki zastosowaniu klasy 'OffsetPagination' można dowolnie określić zakres i ilość wyświetlanych pozycji;
- '/api/webpages/<webpage_id>/: obsługujący metodę GET, wyświetla dane dla strony o podanym id;
- '/api/task/<task_id>/: obsługujący metodę GET, wyświetla obecny stan zleconego zadania asynchronicznego.

Napisałem testy jednostkowe przy użyciu biblioteki unittest i klasy APITestcase. 

Co należy zmienić:
- zlecenie pobrania zdjęć dla istniejącej strony powoduje zdublowanie plików na dysku.

Uwagi:
- aby uruchomić aplikację należy zbudować obraz i uruchomić kontener wpisując w terminalu komendę 'docker-compose up'
- po uruchomieniu kontenera musimy dokonać migracji danych. W oddzielnym oknie terminala wykonujemy komendę 'docker-compose run --rm python bash'. Bedąc w kontenerze tworzymy migracje 'python manage.py makemigrations', a następnie je wykonujemy przy użyciu 'python manage.py migrate'.
