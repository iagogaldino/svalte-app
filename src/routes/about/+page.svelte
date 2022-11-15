<script>
  import { onMount } from "svelte";
  import whatsapp from "$lib/images/whatsapp.png";
  import { page } from "$app/stores";

  const urlAPI = "https://api.store.pede.ai/menu/v2/items?per_page=all&page=1";
  let products = new Array(0);

  page.subscribe((data) => getDetailsMerchant(data.url.searchParams.get("merchant")) );

  function getDetailsMerchant(/** @type {any} */ id) {
    onMount(async () => {
      const response = await fetch(urlAPI + "&merchant_id="+id, { method: "GET" });
      const { categories } = await response.json();
      products = categories.data;
    });
  }

  function onClickWhats() {
    window.open("https://wa.me/5574988420307?text=Ola")
  }

</script>

<svelte:head>
  <title>Merchant Items</title>
  <meta name="description" content="Merchant items app" />
</svelte:head>

<div class="area-categories">
  {#each products as product}
    <div class="categorie" id={product.name}>{product.name}</div>
    <div class="area-items">
      {#each product.items as item}
        <div id={item._id} class="product">
          <div
            class="product-img"
            style="background-image: url({item.photo});"
            alt="Photo"
          />
          <div class="product-data">
            <div class="product-name">{item.name}</div>
            <div>{item.description}</div>
            <div>preco</div>
          </div>
        </div>
      {/each}
    </div>
  {/each}
</div>

<img  class="wwp" src={whatsapp} alt="whatsapp" on:keydown={()=>{}} on:click={() => onClickWhats()} />

<style>
 
  .wwp {
    position: fixed;
    bottom: 0;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    right: 0;
    margin-right: 30px;
    margin-bottom: 10px;
    border: none;
    box-shadow: 0 0 0 0px rgb(247 255 255), 0.3em 0.3em 1em rgb(0 0 0 / 50%);
  }
  .categorie {
    margin-top: 40px;
    font-weight: 600;
  }
  .area-categories {
    background-color: rgb(242, 240, 240);
    padding: 10px;
    margin-top: 20px;
    border-radius: 7px;
  }

  .area-items {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .product {
    width: 100%;
    background-color: white;
    display: grid;
    grid-template-columns: 130px 1fr;
    margin-top: 10px;
    gap: 20px;
    cursor: pointer;
  }

  .product-img {
    height: 130px;
    background-position: center;
    background-size: 100% 100%;
  }

  .product-name {
    font-size: 18px;
    font-weight: 600;
  }

  .product-data {
    padding: 20px;
  }

</style>
