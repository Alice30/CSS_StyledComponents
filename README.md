![](https://s3.amazonaws.com/ckl-website-static/wp-content/uploads/2017/07/Banner_css-1280x680.png)

#CSS style en React

###Comment utiliser CSS pour donner un style à son application React ?

Il existe 3 différentes méthodes d'ajouter du style aux composants :


###Utiliser les classes et fichier CSS :
Utiliser des classes, il suffit d'utiliser un fichier CSS pour cibler les classes.

Exemple :

```
const Button = () => {
	return <button className="button">A button</button>
}

```

```
.button {
	background-color: red;
}

```

On importe le fichier CSS en écrivant :

```
import './style.css'
```


###Utiliser attribut style attaché à JSX élément :

Utiliser l'attribut style attaché à un JSX élément. En utilisant cette deuxième méthode vous n'avez pas besoin d'un fichier CSS séparé.

Exemple :

```
const Button = () => {
	return <button style= {{backgroundColor:'yellow'}}>A button</button>
	}
```
avec cette écriture on utilise les doubles accolades : le style est donc un objet JS.
On peut également écrire le style comme ceci :

```
const buttonStyle = { backgroundColor: 'yellow' }
const Button = () => {
  return <button style={buttonStyle}>A button</button>
} 
```

Quand on utilise ```create-react-app```, les styles styles sont automatiquement préfixés par Autoprefixer.

Le style est écrit en camelCase au lieu des tirets.

**A noter :**

**Les styles ont l'avantage d'être local au composant, donc ils ne peuvent pas affecter d'autres composants de l'app. Ce n'est pas le cas quand on utilise les classes et un fichier externe CSS**

###Utiliser les CSS modules :

(manière d'écrire du CSS qui s'applique seulement a un composant, sans affecter à d'autres élément dans la page).

La troisième option est d'utiliser les CSS modules, c'est un mélange des deux précédentes options traitées ci dessus. En effet, avec CSS modules on utilise des classes, mais la portée du CSS est limité au scope du composant, ce qui signifie que le style qu'on ajoute ne peut pas être appliqué à d'autres composants sans notre permission. De plus, le style est séparé dans un fichier CSS, ce qui est beaucoup plus facile à maintenir plutôt que de maintenir du CSS dans du JS.


Pour utiliser les CSS modules il vous suffit de créer un fichier CSS finissant par ```.module.css```. Puis importer le fichier CSS dans le fichier composant voulu ```import style from './Button.module.css'```, maintenant on peut utiliser le style dans le JSX.

Exemple :

```
const Button = () => {
	return <button className= {style.content}<A button</button>
}
```

En fait, ce qui se passe c'est que React génère une classe spécifique et unique pour chaque composant render, et assigne le CSS à cette classe, donc le CSS n'affecte pas d'autres composants.


 **A noter :**

**Avec la première méthode (les classes/fichier CSS) et la troisième méthode (les CSS modules) on peut utiliser sans configuration SCSS ou SASS. Tout ce qu'il nous suffit de faire c'est de nommer nos fichiers en terminant par ```.scss``` ou ```.sass```**


# Les Styled composants :

Les styles composants sont une des nouvelles manières d'utiliser le CSS dans le JS moderne. Les styles composants sont les futurs sucesseurs du CSS modules.

Les styled composants permettent d'écrire du CSS ou SASS dans les composants sans se préoccuper des collisions de noms de classes.

###Installation :


On peut installer les styled composants en utilisant yarn ou npm, et ajouter dans les fichiers ```import styled from 'styled-components'```.

###Commencer avec styled component :


Styled component enlève le mapping entre components et styles. Cela signifie que quand on défini les styles, on est en réalité en train de créer un composant React normal, qui a les styles rattachés dessus.

Dans cet exemple on créee 2 composant, un wrapper et un title, avec du style rattaché :


```
// Creation d'un composant Title component, qui va render un <h1> avec du style
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// Creation d'un composant Wrapper, qui va render une <section> avec du style
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

// Utilise Title and Wrapper comme n'importe quel autre React composant – sauf qu'ils sont stylisés!
render(
  <Wrapper>
    <Title>
      Hello World!
    </Title>
  </Wrapper>
);
```

```Button```est maintenant un React composant. Nous l'avons créee en utilisant une fonction de styled object, appelé ```button```, et passé quelques propriétés CSS. Ce composant peut maintenant être render dans notre conteneur en utilisant cette syntaxe : ```render(<Button/>)```

Styled composants offrent d'autres fonctions que vous pouvez utilisez pour créer d'autres composants, pas juste ```button```, mais ```section```, ```h1```, ```input``` et plein d'autre.


**On peut remarquer dans l'exemple les tirets qui sont du CSS pure et les backtick qui viennent du JS pure qui sont un moyen de passer un argument à une fonction.**

###Utiliser les props pour personnaliser les composants


Quand on passe des props à un styled composant, ce dernier les passera au DOM node mounted.

Par example, voici comment nous passons le ```placeholder``` et ```type```props à un ```input``` composant :

```

const Input = styled.input`
	//...
	`

render(
	<div>
	  <Input placeholder="..." type="text />
	</div>
)

```

Le résultat de cet exemple est que les props vont être insérées comme des attributs HTML.

Mais au lieu de passer simplement les props au DOM, les props peuvent également être utiliser pour personnaliser un composant.

Exemple :

```
const Button = styled.button`
  background: ${props => (props.primary ? 'black' : 'white')};
  color: ${props => (props.primary ? 'white' : 'black')};
`

render(
  <div>
    <Button>A normal button</Button>
    <Button>A normal button</Button>
    <Button primary>The primary button</Button>
  </div>
) 

```

###Étendre un styled composant existant

Si on a déjà un styled composant et qu'on souhaite en créer un autre similaire, on peut utiliser ```extend```

Exemple :

```
 const Button = styled.button`
   color: black;
`

const WhiteButton = Button.extend`
   color: white;
`

render(
  <div>
    <Button>A black button, like all buttons</Button>
    <WhiteButton>A white button</WhiteButton>
  </div>
)

```
The styled method works perfectly on all of your own or any third-party components, as long as they attach the passed className prop to a DOM element.

**Dans les styled composant on peut utiliser les media queries, nesting, SASS**

###Sources utilisées :

 <https://www.styled-components.com/docs/basics>
 <https://flaviocopes.com/>
