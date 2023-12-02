# Creació del primer contenidor amb Docker

**Pas 1**: Creació de l'estructura de nostre primer projecte

Comandes a executar:

```
mkdir ~/c01-pagina-web
cd ~/c01-pagina-web
```

**Pas 2**: Creació del fitxer **```index.html```** amb el següent contingut:

Comandes a executar:

```
vi ~/c01-pagina-web/index.html
```


```html 
<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sóc el títol de la pàgina</title>
</head>
<body>
 
    <header>
      <h1>Benvingut al nostre lloc web!</h1>
      <p>Aquí teniu el nostre logotip i eslògan.</p>
    </header>
     
    <nav>
      <header>
        <h2>Tria el teu interès</h2>
      </header>
      <ul>
        <li>Menu 1</li>
        <li>Menu 2</li>
        <li>Menu 3</li>
      </ul>
    </nav>
     
    <article>
      <header>
        <h1>Títol de l'article</h1>
        <h2>Subtítol de l'article</h2>
      </header>
       
      <section>
        <h4>Primera part lògica (p. ex., "Teoria")</h4>
        <p>Paràgraf 1 del primer apartat</p>
         
        <h5>Un altre subtítol de la primera secció</h5>
        <p>Paràgraf 2 del primer apartat</p>
      </section>
       
      <section>
        <h4>Segona part lògica (p. ex., "Pràctica")</h4>
        <p>Paràgraf 1 de l'apartat segon</p>
        <p>Paràgraf 2 de l'apartat segon</p>
      </section>
     
      <footer>
        <h5>Biografia de l'autor</h5>
        <p>Paràgraf al peu de pàgina de l'article</p>
      </footer>
     
    </article>
     
    <aside>
       
      <h2>Coneix-nos millor</h2>
       
      <section>
        <h4><i>Posts</i> populars</h4>
        <ul>...</ul>
      </section>
       
      <section>
        <h4>Socis</h4>
        <ul>...</ul>
      </section>
       
      <section>
        <h4>Testimonis</h4>
        <ul>...</ul>
      </section>
     
    </aside>
     
    <footer>
      <ul>
        <li>Copyright</li>
        <li>Enllaços a xarxes socials</li>
      </ul>
    </footer>
   
  </body>
</html>
```


