Introduction
============

Comme **Java** et **.Net**, **Scala** support aussi les annotations, que
vous avez probablement déjà vu, ces annotations permettent d’ajouter des
informations sémantiques appelés métadonnées, ces derniers ajoutent un
niveau d’information supplémentaire au code source du programme, mais
elles n’ont pas d’effets directs sur les entités qu’elles concernent.

Ces fameuses données sémantiques peuvent être lues par des programmes
comme des générateurs de documentation **ScalaDoc**, mais elles sont
aussi lues par le compilateur.

Un simple exemple des annotations que avez probablement déjà vu est
**@override**, qu’on utilise en **Java** par exemple pour définir une
méthode qui est héritée de la classe parente. On ne l’utilise donc que
dans le cas de l’héritage. En plaçant ce mot-clé avant l’implémentation
de la méthode réécrite, le compilateur vérifiera que la méthode est
correctement utilisée (mêmes arguments, même type de valeur de retour)
et affichera un message d’avertissement si ce n’est pas le cas.

Ce tutoriel vous montre comment utiliser les annotations en **Scala**.
Il montre aussi leurs syntaxe générale, et le rôle de quelque
annotations standards.

L’utilisation des annotations
=============================

Afin d’aider les développeur à produire un code propre, lisible et
documenté, l’utilisation des annotations concernent les fonctionnalités
suivantes :

Génération de la documentation ScalaDoc
---------------------------------------

Les annotations permettent de simplifier considérablement le processus
de documentation des programme, car elles sont intégrés directement dans
le code, et il n’est pas nécessaire de créer et maintenir les fichiers
externes comme ScalaDoc.

Génération du code
------------------

Quelques annotations permettent de respecter certains conventions de
dénomination, vous allez trouver l’exemple de @scala.beans.BeanProperty
dans la partie annotation standards de ce tutoriel, qui permet de
respecter la convention de dénomination des getters et setters.

Vérifier l’existence des erreurs dans le code
---------------------------------------------

Les annotations aident les développeurs à détecter les erreurs qu’ils
ont fait, comme l’ouverture d’un fichier sans le fermer.

syntaxe des annotations
=======================

Les annotations sont autorisées sur tout type de déclaration, comme les
classes, les méthodes, les interfaces, les variables, et elles peuvent
avoir des paramètres en entré, de plus elles doivent obligatoirement
précéder les entité qu’elles annottent, et plusieurs annotations peuvent
être utilisés pour le même type de déclaration sans considérer l’ordre.\

La forme générale des annotations est la suivante :

### @annot(exp1,exp2,...,expN)

***- annot** specifie la classe de l’annotation (le nom)** - ex**
specifie les paramêtres de l’annotation*

[tab1]

<span>|l|l|</span> Type de déclaration & Exemple d’annotation\

Annotation des méthodes & ***@deprecated*** def methode()= …\
Annotation des classes & ***@serializable*** class NomDeLaClasse<span>
... </span>\
Annotation des expression & … (X : ***@unchecked***) match<span> ...
</span>\
annotation des types & String ***@local***\
annotation des variables & ***@trasient*** var variable: Int\

Les annotations standards
=========================

Scala comprend plusieurs types annotations standards dont **Java
Platform**, **Java Beans**, **Deprecation**, et **Scala Compiler**, dans
cette partie je vais vous citer quelques exemple dans chaque type
d’annotation :

Les annotation de Java Platform en Scala
----------------------------------------

Les annotations permettent de simplifier considérablement le processus
de documentation des programme, car elles sont intégrés directement dans
le code, et il n’est pas nécessaire de créer et maintenir les fichiers
externes comme ScalaDoc.

-   **@transient**: permet d’interdire la sérialisation de certaines
    variables d’une classe.

-   **@volatile** : est utilisé sur les variables qui peuvent être
    modifiées de manière asynchrone. C’est-à-dire que plusieurs threads
    peuvent y accéder simultanément.

-   **@throws(exception)** : est utilisé pour déclarer qu’une exception
    peut être levées.

**Exemple d’utilisation de l’annotation @throws :\
**

L’exception **UnsupportedAudioFileException** peut être levée lors de
l’utilisation de la *fonction jouerLaMusic()* dans le code suivant :

![l’utilisation de l’annotation @throws pour lever une
exception](image0.png "fig:") [fig1]

Les annotations de Java Beans en Scala
--------------------------------------

En ce qui concerne les annotations de **Java Beans** en Scala, leurs
utilisation aide le développeur à respecter les conventions de
dénomination pour définir les “attributs” d’un bean, comme les getters
et les setters. Pour l’exemple on peut citer les deux annotations
suivantes :

-   **@scala.beans.BeanProperty** : à pour but d’ajouter les getters et
    les setters (*getX*, *setX*) à la classe concernée.

-   **@scala.beans.BooleanBeanProperty** : à le même but que
    l’annotation précédente, sauf qu’elle renomme les getters en **isX**
    si le type de la variable est boolean.

L’annotation “deprecated”
-------------------------

Parfois, on écrit une méthode que nous souhaitons enlever plus tard,
mais une fois implémenté, le code écrit par d’autres personnes peut
appeler la méthode. Par conséquent, nous ne pouvons pas simplement
supprimer la méthode, car cela empêcherait la compilation du code des
autres qui l’utilisent.\

l‘annotation **@Deprecated** nous permettent de supprimer gracieusement
une méthode ou une classe qui s’avère être une erreur. Nous marquions la
méthode ou la classe comme obsolète, puis toute personne qui appelle
cette méthode ou cette classe recevra un avertissement comme quoi il ne
faudrait plus l’utiliser.\

Alors L’idée est qu’après quelque temps suffisant, nous pouvons supposer
que tous les développeurs ont cessé d’accéder à la classe ou à la
méthode obsolète et que nous pouvons donc la supprimer en toute
sécurité.\

Nous marquions une méthode comme étant obsolète en écrivant simplement
**@deprecated** avant celle-ci.\

**Par exemple:**

![l’utilisation de l’annotation @deprecated](image1.png "fig:") [fig2]

Ce code se compile, mais un avertissement va s’afficher pour nous
informer que la fonction utilisé est obsolète.

![le warning est affiché par le compilateur](image2.png "fig:") [fig3]

Les annotations du compilateurs Scala
-------------------------------------

Dans cette partie on va prendre l’exemple de l’annotation **@unchecked**
qui appartient aux annotation du compilateur Scala, cette annotation
permet de banaliser les avertissements, comme dans le cas des sélecteurs
“pattern matching”, qui ne sont pas exhaustives. Pour sentir l’impact de
l’utilisation de cette annotation, le code suivant est une application
d’un sélecteur non exhaustif sans l’utilisation de **@unchecked** :

Après avoir lancer le code ci-dessus, le compilateur génère un
avertissement.\

Mais lorsqu’on ajoute l’annotation **@unchecked** devant X, le
compilateur ne génère plus d’avertissement.

![Selecteur non exhaustif avec l’annotation
@unchecked](image5.png "fig:") [fig4]

### Remarque 

:Par manque de temps, la liste des annotations standards présentés dans
ce tutoriel n’est pas exhaustive, mais ça vous donne une idée claire sur
les annotations prédéfinis en Scala, pour plus d’annotations standards
consultez le lien de la documentation officielle suivant
:**ww.scala-lang.org/api/2.12.0-M5/scala/annotation/index.html**
