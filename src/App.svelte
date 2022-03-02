<script>
	let name = "Aurélio";


	let images=[
		{
			path:"https://pbs.twimg.com/profile_images/1121395911849062400/7exmJEg4_400x400.png",
			description: "Primeira Imagem"
		},

		{
			path:"https://yt3.ggpht.com/_q52i8bUAEvcb7JR4e-eNTv23y2A_wg5sCz0NC0GrGtcw1CRMWJSOPVHUDh_bngD0q4gMvVeoA=s900-c-k-c0x00ffffff-no-rj",
			description: "Segunda Imagem"
		}
	];

const [imgObj1, imgObj2] = images;


let count = 0;                 //botão
const clickHandler = () => {   //para
	count++                    //aumentar
};                             //o contador
$: doubled = count*2;          //$: é usado para calcular o doubled a partir de outra variável (neste caso, count). Quando o
                               //count modificar, o doubled tb muda.
$: if (count == 10) {
	alert('Contagem está perigosamente alta!');
	count = 9;
};


let timeArray=[];
let timeObject={};
const clickHandler2 = () => {
	const d = new Date();
	timeArray=[...timeArray, d.getTime()]; //para acrescentar algo no array, precisamos usar essa notação array=[...array, ELEMENTO]
	timeObject={...timeObject,[d.getTime()]:d.toLocaleTimeString()}; //o mesmo para objetos.
};


import Compo1 from './components/Compo1.svelte';
const data = [
       {title: "Title1", subtitle:"Subtitle1"},
       {title: "Title2", subtitle:"Subtitle2"}
   ];

const[card1, card2] = data;

let list = [
	{id:1, title:"Primeiro Card", subtitle:"Subtitle do primeiro card"},
	{id:2, title:"Segundo Card", subtitle:"Subtitle do segundo card", membersOnly: true},
	{id:3, title:"Terceiro Card", subtitle:"Subtitle do terceiro card"},
	{id:4, title:"Quarto Card", subtitle:"Subtitle do quarto card", membersOnly: true},
	{id:5, title:"Quinto Card", subtitle:"Subtitle do quinto card"},
	{id:6, title:"Sexto Card", subtitle:"Subtitle do sexto card", membersOnly: true}
];

</script>


<main class="container">

	<div class="topic">
		<h1>Olá { name } </h1>
		<img class="img" src={imgObj1.path} alt={imgObj1.description}/>
		<img class="img" src={imgObj2.path} alt={imgObj2.description}/>
	</div>

	<div class="topic">
		<button	on:click={clickHandler}>Click me!</button>
		<p>count: {count}</p>
		<p>doubled: {doubled}</p>
		

		<button on:click={clickHandler2}>Also click me!</button>
		<p>Array: {JSON.stringify(timeArray)}</p>
		<p>Object: {JSON.stringify(timeObject)}</p>
	</div>

	<div class="topic">
		<Compo1/>
		<Compo1 title="Título modificado aqui dentro"/> <!-- no Compo1 eu dei export antes da variável title. Assim ela pode ser
														modificada dentro deste componente que importou Compo1. -->
		<Compo1 {...card1}/> <!-- coloca card1 como propriedade de Compo1. card1 é um objeto com title e subtitle, então ele define
							essas propriedades de forma mais simples-->
		<Compo1 {...card2}/>


		{#each list as item}      <!--Percorre o array list, chamando cada elemento de item. para cada um...-->
			<Compo1 {...item} on:cardClicked={ev => console.log(ev.detail.id)} />  <!--Cria uma elemento Compo1 e insere o item como propriedade dele.-->
		{/each}                                                          <!-- observa que usei o evento cardClicked, criado no Compo01-->
	</div>

</main>

<style>
	.container{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.img{
		width: 25%;
	}

	.topic{
		margin: 2rem 0;
		border: 1px solid;
	}
</style>