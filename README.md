# Infos
## Symfony Komponenten 
Pakete, die Kernfunktionen und Abstraktionen auf niedriger Ebene implementieren, die die meisten Anwendungen benötigen (Routing, Konsole, HTTP-Client, Mailer, Cache, ...)
## Symfony Bundles
Pakete, die High-Level-Funktionen hinzufügen oder Integrationen mit Bibliotheken von Drittanbietern anbieten
## Lifecycle von Doctrine Objekten
Beim Erstellen eines neuen Kommentars wäre es gut, wenn das createdAt-Datum automatisch auf das aktuelle Datum und die aktuelle Uhrzeit gesetzt würde.

Doctrine hat verschiedene Möglichkeiten, Objekte und deren Properties (Eigenschaften) während ihres Lifecycle zu manipulieren (bevor die Zeile in der Datenbank erstellt wird, nachdem die Zeile aktualisiert wird, ...).
### Lifecycle-Callbacks definieren
Wenn das Verhalten nicht von einem Service abhängt und nur auf eine bestimmte Entity angewendet werden soll, definierst Du einen Callback in der Entity-Klasse:
``` php
+++ b/src/Entity/Comment.php
use Doctrine\ORM\Mapping as ORM;

/**
* @ORM\Entity(repositoryClass=CommentRepository::class)
* @ORM\HasLifecycleCallbacks()
*/
class Comment
{
    /**
     * @ORM\PrePersist
     */
    public function setCreatedAtValue()
    {
        $this->createdAt = new \DateTime();
    }
}
```

Das ``@ORM\PrePersist-Event`` wird ausgelöst, wenn das Objekt zum ersten Mal in der Datenbank gespeichert wird. In diesem Fall wird die ``setCreatedAtValue()-Methode`` aufgerufen und das aktuelle Datum und die aktuelle Uhrzeit für den Wert der ``createdAt-Property/Spalte`` verwendet.


# dependencies
- `profiler --dev`
- `logger`
- `debug --dev`
- `maker --dev`
- `annotations`
- `orm:^2`
- `admin:^3`
- `twig`
- `twig/intl-extra:^3`
- `validator`
- `string`
- `mime`
- `security`
- `phpunit --dev`