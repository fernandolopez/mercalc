<script>
    import { resolve } from '$app/paths';
    let product = $state("Producto")
    let units = $state(1)
    let kilograms = $state(1)
    let price = $state()
    let price_pk = $state()
    let items = $state([])
    let warning = $state()

    function calc() {
        if (units && kilograms && price) {
            price_pk = (price / (units * kilograms)).toFixed(2)
        }
        warning = null
    }

    function add() {
        if (!product || !units || !kilograms || !price) {
            warning = "Por favor complete todos los campos"
            return
        }
        warning = null
        items = [...items, { product, units, kilograms, price, price_pk }]
        product = ""
        units = 1
        kilograms = 1
        price = ""
        price_pk = ""
    }
</script>
<p>
    <a href={resolve('/')}>Volver</a>
</p>
<form>
    <ul>
        <li>
            <label for="product">Producto</label>
            <input id="product" type="text" bind:value={product}/>
        </li>
        <li>
            <label for="unidades">Unidades</label>
            <input id="unidades" type="text" bind:value={units} on:input={calc}/>
        </li>
        <li>
            <label for="kilogramos">Kilogramos por unidad</label>
            <input id="kilogramos" type="text" bind:value={kilograms} on:input={calc}/>
        </li>
        <li>
            <label for="precio">Precio</label>
            <input id="precio" type="text" bind:value={price} on:input={calc}/>
        </li>    
    </ul>
</form>
<p>Precio por kilogramo: {price_pk}</p>
<button on:click={add}>Agregar</button>
<p>{warning}</p>

<table>
    <thead>
        <tr>
            <th>Producto</th>
            <th>Unidades</th>
            <th>Kilogramos por unidad</th>
            <th>Precio</th>
            <th>Precio por kilogramo</th>
        </tr>
    </thead>
    <tbody>
        {#each items as item}
            <tr>
                <td>{item.product}</td>
                <td>{item.units}</td>
                <td>{item.kilograms}</td>
                <td>{item.price}</td>
                <td>{item.price_pk}</td>
            </tr>
        {/each}
    </tbody>
</table>
    