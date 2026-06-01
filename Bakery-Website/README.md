# Static Webpage — WAR source

Static bakery landing page, structured as a Maven webapp project so you can build the WAR yourself.

## Project layout

```
maison-levain-src/
├── pom.xml
└── src/
    └── main/
        └── webapp/
            ├── index.html          # full page (HTML + inline CSS + Google Fonts)
            ├── assets/             # 4 bakery images
            │   ├── bakery-hero.jpg
            │   ├── bakery-croissant.jpg
            │   ├── bakery-sourdough.jpg
            │   └── bakery-cake.jpg
            └── WEB-INF/
                └── web.xml         # Jakarta EE 6 descriptor (WildFly 27+)
```

No Java source — it's a pure static webapp packaged as a WAR.

## Build

Requires JDK 11+ and Maven 3.6+.

```bash
mvn clean package
```

Output: `target/maison-levain.war`

## Deploy to WildFly

Copy the WAR into the deployments folder:

```bash
cp target/maison-levain.war $WILDFLY_HOME/standalone/deployments/
```

Then visit `http://<host>:8080/maison-levain/`.

To serve it at the root context, rename to `ROOT.war`:

```bash
cp target/maison-levain.war $WILDFLY_HOME/standalone/deployments/ROOT.war
```

## Older WildFly / Java EE (javax.*)

`web.xml` uses the Jakarta EE namespace (`jakarta.servlet`, WildFly 27+).
For older servers using `javax.*`, edit `src/main/webapp/WEB-INF/web.xml`:

- `xmlns` → `http://xmlns.jcp.org/xml/ns/javaee`
- `version` → `4.0`
