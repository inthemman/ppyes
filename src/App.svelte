<script>
	async function callDollah() {
    let dollah = await fetch('https://quotation-api-cdn.dunamu.com/v1/forex/recent?codes=FRX.KRWUSD').then(function(res){return res.json()})
		hwan = dollah[0].cashBuyingPrice
	}
	let fee = 3.5
	let hwan;
	let name;
	let price;
	let orders = [];
	function addUser() {
		orders = [...orders,{
		name : name,
		price : price,
		kprice : price * hwan
	}]
		console.log(orders);
	}
</script>

<div>hwan<input type=number bind:value={hwan}><button on:click={callDollah}>
	auto
	</button></div>
<div>delivery<input type=number bind:value={fee}></div>
<div>Name:<input type=text bind:value={name}></div>
<div>Price:<input type=number step=any min=1 bind:value={price}></div>
<button on:click={addUser}>
	add
</button>
<ul>
	{#each orders as {name,price,kprice},i}
	<li>
		{name} : ${price},{kprice},result : {kprice + (fee * hwan) / orders.length} <button on:click={function(i) {
														 orders.splice(i,1);
														 orders = orders;
														 }}>
		remove
		</button>
	</li>
	{/each}
</ul>
