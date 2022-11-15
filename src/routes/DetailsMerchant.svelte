<script async script>
  import { onMount } from "svelte";
  import Skeleton from "svelte-skeleton-loader";

  const urlAPI = "https://api.store.pede.ai/merchant/v1/merchants?area_id=60d52c47637de64049094420&sort_by=delivery_rate&payment_types=&card_brands=&get_all=true";
  let merchant = {
    old_id: "",
    name: "",
    rating: "",
    delivery_estimation: "",
    minimum_order: "",
    disabled_ordering: "",
    free_delivery_fee_above_price: "",
    logo_url: "",
    is_open: true,
    delivery_fee: "",
    has_offer: "",
    favorite: "",
  };

  let items = new Array(10).fill(merchant);
  
  onMount(async () => {
    const response = await fetch(urlAPI,
      {
        method: "GET"
      }
    );
    const data = await response.json();
    items = data.merchants;
  });


  const  onClickMerchant = (/** @type {any} */ a) => {
    a._id? window.location.href="/about?merchant=" + a._id : ''
  }
 

</script>

<div class="content">
  {#each items as item, key}
      <div class="item" on:keydown={()=>{}} on:click={() => onClickMerchant(item)}>
        <div class="logo" style="background-image:url({item.logo_url})" />
        <div class="data">
          <div class={item.name ? "" : "skeleton"}>{item.name}</div>
          <div class={item.name ? "" : "skeleton"}>
            {item.delivery_estimation}
          </div>
          <div class={item.name ? "" : "skeleton"}>
            {#if item.name}R${item.delivery_fee},00{/if}
          </div>
        </div>
      </div>
  {/each}
</div>

 
<style>

  .content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 30px;
  }
  .item {
    display: grid;
    grid-template-columns: 115px 1fr;
    width: 426px;
    background-color: rgb(255, 255, 255);
    height: 115px;
    border-radius: 7px;
    cursor: pointer;
    border: solid 1px white;
  }

  .item:hover {
    box-shadow: 0 0 0 0px rgb(247 255 255), 0.3em 0.3em 1em rgb(0 0 0 / 14%);
  }

  .logo {
    border-radius: 7px 0px 0px 7px;
    background-size: 100% 100%;
  }

  .data {
    display: grid;
    padding: 10px;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    border-radius: 7px;
  }

  .data div:nth-child(1) {
    font-weight: 600;
  }

  @keyframes skeleton-loading {
    0% {
      background-color: hsl(200, 20%, 80%);
    }
    100% {
      background-color: hsl(200, 20%, 95%);
    }
  }

  .skeleton {
    animation: skeleton-loading 1s linear infinite alternate;
    height: 8px;
  }
</style>
