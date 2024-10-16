# Lucrare de laborator nr. 2. Cereri HTTP și șablonizare în Laravel

### Scopul lucrării
Scopul acestei lucrari de laborator este sa se studieze principiile de bază ale lucrului cu cererile HTTP în Laravel și șablonizarea folosind Blade, pe baza unei aplicații web „To-Do App pentru echipe” — o aplicație pentru gestionarea sarcinilor în cadrul unei echipe.
Aplicația este destinată unei echipe care dorește să își gestioneze sarcinile, să le atribuie membrilor și să monitorizeze starea și prioritatea sarcinilor (similar cu Github Issues).

### Descrierea lucrarii individuale


### Documentatie scurtă a proiectului



## Nr. 1. Pregătirea pentru lucru, instalarea Laravel
#### 1. Deschidem terminalul și cream un nou proiect Laravel cu numele todo-app folosind Composer: composer create-project laravel/laravel:^10 todo-app
![image](https://github.com/user-attachments/assets/7b0384f6-e6d4-4c21-a229-407df1749cad)
#### 2. Intram în directorul proiectului: cd todo-app
![image](https://github.com/user-attachments/assets/ac539ecb-3c9a-4b89-928d-ef8d45bc90cd)
#### 3. Pornim serverul încorporat Laravel: php artisan serve
![image](https://github.com/user-attachments/assets/f37b52bc-952e-46fa-a257-2a71e89656ad)
#### Ce vedem în browser când deschidem pagina http://localhost:8000?
![image](https://github.com/user-attachments/assets/4d615a1a-36fc-432c-924f-0ac6e63207f3)







## Nr. 2. Configurarea mediului
#### 1. Deschidem fișierul .env și setați următoarele configurări ale aplicației: ini APP_NAME=ToDoApp APP_ENV=local APP_KEY= APP_DEBUG=true APP_URL=http://localhost:8000
![image](https://github.com/user-attachments/assets/af1f3231-9255-419b-aea7-89e6cc65a9c1)
#### 2. Generam cheia aplicației, care va fi utilizată pentru criptarea datelor: php artisan key:generate
![image](https://github.com/user-attachments/assets/bd059458-1f4d-4559-adea-19283d022127)
#### Ce s-ar întâmpla dacă această cheie ar ajunge pe mâna unui răufăcător?






## Nr. 3. Principiile de bază ale lucrului cu cererile HTTP


### Nr. 3.1. Crearea rutelor pentru pagina principală și pagina "Despre noi"
#### 1. Cream un controller HomeController pentru gestionarea cererilor către pagina principală.
![image](https://github.com/user-attachments/assets/3b5f1885-71f6-448b-83c2-2ee31b1b36d1)
#### 2. Adăugam metoda index în HomeController, care va afișa pagina principală.
![image](https://github.com/user-attachments/assets/80dc0d6f-f150-4fae-ac09-78aa6e4f7ece)
#### 3. Cream ruta pentru pagina principală în fișierul routes/web.php. php public function index() { return view('home'); }
![image](https://github.com/user-attachments/assets/572650a2-d9f7-4704-a474-ddbc92b721d1)
#### 4. Deschidem browserul și accesați adresa http://localhost:8000. Ne asiguram că pagina goală se încarcă, deoarece vizualizarea home.blade.php nu a fost încă creată.
![image](https://github.com/user-attachments/assets/69f1ecf5-1fc6-43e5-a80a-ca8f7b79fb5b)
#### 5. În același controller HomeController, cream o metodă pentru pagina "Despre noi".
![image](https://github.com/user-attachments/assets/8aae4ae1-f63a-417b-9742-d26d5fe81912)
#### 6. Adăugam ruta pentru pagina "Despre noi" în fișierul routes/web.php.
![image](https://github.com/user-attachments/assets/8904b63a-8b5c-4e48-be87-8728420ea9af)



### Nr. 3.2. Crearea rutelor pentru sarcini
#### 1. Cream un controller TaskController pentru gestionarea cererilor legate de sarcini și adăugam următoarele metode:
 - index — afișarea listei de sarcini;
 - create — afișarea formularului pentru crearea unei sarcini;
 - store — salvarea unei sarcini noi;
 - show — afișarea unei sarcini;
 - edit — afișarea formularului pentru editarea unei sarcini;
 - update — actualizarea sarcinii;
 - destroy — ștergerea sarcinii.
   
Creare:
![image](https://github.com/user-attachments/assets/f649fe8e-0dbf-4ada-a718-46a5024a76b0)
![image](https://github.com/user-attachments/assets/bb08d178-b18f-4566-960e-a276ed7e2c85)

Crearea functiilor si metodelor:
![image](https://github.com/user-attachments/assets/5f2531d7-d4d4-43ad-b75e-836805b6853e)
![image](https://github.com/user-attachments/assets/8bc09ec4-21c7-4e28-b513-fac7fb010502)

#### 2. Cream rutele pentru metodele controllerului TaskController în fișierul routes/web.php și specificați metodele HTTP corecte pentru fiecare rută.
#### 3. Utilizam gruparea rutelor pentru controllerul TaskController cu prefixul /tasks pentru a simplifica rutarea și a îmbunătăți lizibilitatea codului.
#### 4. Definim nume corecte pentru rutele controllerului TaskController
#### 5. Adăugam validarea parametrilor rutei id pentru sarcini. Asigurați-vă că parametrul id este un număr întreg pozitiv. Utilizați metoda where pentru a limita valorile parametrului id.
![image](https://github.com/user-attachments/assets/f4ee1eb5-7939-4f18-a37e-39ecbd98d4aa)
#### 6. În loc să cream manual rute pentru fiecare metodă, putem folosi un controller de resurse, care va crea automat rute pentru toate operațiunile CRUD: În fișierul routes/web.php, înlocuim crearea manuală a rutelor pentru controllerul TaskController cu un controller de resurse: php Route::resource('tasks', TaskController::class);
![image](https://github.com/user-attachments/assets/662b7c98-ddb9-4caf-8bcb-806c9baa2873)

#### Diferența între crearea manuală a rutelor și utilizarea unui controller de resurse:
#### Ce rute și ce nume de rute vor fi create automat?

#### 7. Verificam rutele create cu ajutorul comenzii php artisan route:list.
![image](https://github.com/user-attachments/assets/18f0b301-ed55-4f05-801b-ac7b51babbf2)








   
## Nr. 4. Șablonizarea folosind Blade
### Nr. 4.1. Crearea unui layout pentru pagini
#### 1. Cream un layout pentru paginile principale layouts/app.blade.php cu următoarele elemente comune ale paginii:
 - Titlul paginii;
 - Meniu de navigare;
 - Conținutul paginii.
#### 2. Folosim directiva @yield pentru a defini zona în care va fi inserat conținutul diferitelor pagini.
![image](https://github.com/user-attachments/assets/4836d62f-5182-4414-acd1-f59957858b4c)




### Nr. 4.2. Utilizarea șabloanelor Blade
#### 1. Cream, vizualizarea pentru pagina principală home.blade.php folosind layoutul layouts/app.blade.php în directorul resources/views.
#### 2. Pe pagina principală sunt:
 - Mesaj de bun venit: titlu și o scurtă descriere a aplicației, de exemplu „To-Do App pentru echipe”.
 - Navigație: linkuri către secțiunile principale, cum ar fi: Lista de sarcini; Crearea unei sarcini.
 - Informații despre aplicație: o scurtă descriere a scopului aplicației și a principalelor sale funcții.
![image](https://github.com/user-attachments/assets/320ade8d-5899-4cd5-ab6e-5498dbbcdc42)

#### 3. Cream vizualizarea pentru pagina "Despre noi" — about.blade.php folosind layoutul layouts/app.blade.php în directorul resources/views.
![image](https://github.com/user-attachments/assets/46425fb9-d685-4eb2-936d-2d437e9cf775)

#### 4. Cream vizualizări pentru sarcini cu următoarele șabloane în directorul resources/views/tasks:
 - index.blade.php — lista de sarcini;
 - show.blade.php — afișarea unei sarcini;
#### 5. Randam lista de sarcini pe pagina index.blade.php folosind date statice transmise din controller cu ajutorul directivei @foreach.
![image](https://github.com/user-attachments/assets/2e0bc365-478a-4e78-9361-249bca0df8a8)
![image](https://github.com/user-attachments/assets/8bf01ca4-c9f1-4b52-8b5a-21627ed3b676)



### Nr. 4.3. Componente anonime Blade
#### 1. Cream o componentă anonimă pentru afișarea antetului (header). Folosiți componenta creată în layoutul layouts/app.blade.php.
![image](https://github.com/user-attachments/assets/cb240377-e0ae-431f-b79f-7838ba7afd7b)

#### 2. Cream o componentă anonimă pentru afișarea sarcinilor:

Componenta trebuie să fie simplă și să folosească parametri transmiși prin directiva @props. Acest lucru va face șabloanele mai flexibile și reutilizabile pe diverse pagini.

Componenta trebuie să afișeze informații despre sarcină:
 - Titlul sarcinii;
 - Descrierea sarcinii;
 - Data creării sarcinii;
 - Data actualizării sarcinii;
 - Acțiuni asupra sarcinii (editare, ștergere);
 - Starea sarcinii (finalizată/nu este finalizată);
 - Prioritatea sarcinii (scăzută/medie/ridicată);
 - Responsabilul sarcinii (Assignment), adică numele utilizatorului căruia i-a fost atribuită sarcina.
#### 3. Afișam componenta de sarcină creată pe pagina show.blade.php folosind parametrii transmiși.


### Nr. 4.4. Stilizarea paginilor
#### 1. Adăugam stiluri pentru pagini folosind CSS sau preprocesatoare (de exemplu, Sass sau Less).
#### 2. Cream un fișier de stiluri app.css în directorul public/css și includeți-l în layoutul layouts/app.blade.php.
#### 3. Adăugam stiluri pentru elementele paginii, cum ar fi titluri, meniuri de navigare, butoane, formulare etc.
#### 4. Opțional, putem folosi biblioteci de stiluri, cum ar fi Bootstrap sau Tailwind CSS.






## Nr. 5. Sarcini suplimentare
#### 1. Afișam ultima sarcină creată pe pagina principală folosind View Composer.
#### 2. Cream o componentă anonimă suplimentară pentru afișarea priorității sarcinii (scăzută, medie, ridicată) cu culori sau pictograme diferite pentru fiecare prioritate.






### Răspunsuri la întrebările de control
#### Ce este un controller de resurse în Laravel și ce rute creează?
Un controller in Laravel este o clasa care gestioneaza cererile prin metode dedicate. Fiecare metoda din controller este responsabila de o actiune specifica, apelata printr-o ruta. In loc sa plasam logica de procesare direct in rute, aceasta poate fi mutata in metodele controllerului, facand astfel codul mai organizat si usor de intretinut.

Laravel este un tip de controller care gestioneaza operatiunile CRUD (Create, Read, Update, Delete) pentru un model. Laravel creeaza automat rute pentru aceste operatiuni atunci cand folosesti Route::resource. Rutele includ: index, create, store, show, edit, update, si destroy.

#### Explicați diferența între crearea manuală a rutelor și utilizarea unui controller de resurse.
Crearea manuala a rutelor implica definirea fiecarui endpoint si metoda in mod individual. Utilizarea unui controller de resurse simplifica procesul prin generarea automata a tuturor rutelor necesare pentru operatiunile CRUD, reducand astfel volumul de cod si mentenanta.

#### Ce avantaje oferă utilizarea componentelor anonime Blade?
 - Usurinta in utilizare, nu necesita clase PHP dedicate.
 - Reutilizare mai simpla a codului in mai multe vizualizari.
 - Mai putina configurare si structura mai curata pentru componentele simple.

#### Ce metode de cereri HTTP sunt folosite pentru a executa operațiunile CRUD?
 - Create: POST
 - Read: GET
 - Update: PUT/PATCH
 - Delete: DELETE







### Concluzii
Concluziile generale ale acestei lucrari de laborator evidentiaza importanta utilizarii corecte a controllerelor si componentelor in Laravel pentru a construi aplicatii web structurate si eficiente. Prin folosirea unui controller de resurse, am observat o simplificare semnificativa a gestionarii operatiunilor CRUD, automatizand crearea rutelor si reducand efortul de scriere manuala a acestora. Comparand abordarea manuala cu cea bazata pe controllere de resurse, am putut aprecia eficienta si claritatea oferita de Laravel.

De asemenea, am inteles ca utilizarea componentelor anonime Blade aduce un plus de flexibilitate in dezvoltarea aplicatiilor, oferind o modalitate mai simpla de a organiza si reutiliza codul vizual. In final, intelegerea metodelor de cereri HTTP corelate cu fiecare operatiune CRUD este esentiala pentru implementarea corecta a operatiunilor pe server, respectand bunele practici in dezvoltarea aplicatiilor RESTful.
