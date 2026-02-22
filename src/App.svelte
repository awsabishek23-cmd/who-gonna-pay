<script >
    let user = $state("")
    let users = $state([])
    let payer = $state("")
    let resultOpposite = $state(true)
    const handleSubmit = (e) => {
        e.preventDefault()
        if(user){
          users.push(user)
        }
        user = ""
    }
    const handleDelete = (index) => users.splice(index,1)
    
    const handlePay = () => {
      payer = users[Math.round(Math.random() * (users.length - 1))]
      resultOpposite = !resultOpposite
    }
    
</script>

<div class="flex justify-center">
  <div class="container max-w-5xl px-3 mt-9">
    <!-- svelte-ignore a11y_consider_explicit_label -->
      {#if resultOpposite}
        <div>
          <p class="text-center text-3xl">who gonna pay!</p>
          <form onsubmit={handleSubmit}>
              <input type="text" bind:value={user} class="border-b-2 outline-none w-full text-2xl" placeholder="Enter people"><br>
              <div class="flex justify-end-safe">
                <button class="cursor-pointer mt-2">
                  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#000000"><path d="M720-400v-120H600v-80h120v-120h80v120h120v80H800v120h-80ZM247-527q-47-47-47-113t47-113q47-47 113-47t113 47q47 47 47 113t-47 113q-47 47-113 47t-113-47ZM40-160v-112q0-34 17.5-62.5T104-378q62-31 126-46.5T360-440q66 0 130 15.5T616-378q29 15 46.5 43.5T680-272v112H40Zm80-80h480v-32q0-11-5.5-20T580-306q-54-27-109-40.5T360-360q-56 0-111 13.5T140-306q-9 5-14.5 14t-5.5 20v32Zm296.5-343.5Q440-607 440-640t-23.5-56.5Q393-720 360-720t-56.5 23.5Q280-673 280-640t23.5 56.5Q327-560 360-560t56.5-23.5ZM360-640Zm0 400Z"/></svg>
                </button>
              </div>
          </form>
          
          
          {#each users as user, index (index)}
            <div class="flex justify-between items-center pt-5 px-0.75">
              <p class="text-2xl">{user}</p>
              <button onclick={() => handleDelete(index)} class="cursor-pointer">
              <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#000000"><path d="M280-120q-33 0-56.5-23.5T200-200v-520h-40v-80h200v-40h240v40h200v80h-40v520q0 33-23.5 56.5T680-120H280Zm400-600H280v520h400v-520ZM360-280h80v-360h-80v360Zm160 0h80v-360h-80v360ZM280-720v520-520Z"/></svg>
              </button>
            </div>
          {/each}
          
          {#if users.length > 1}
            <div class="flex justify-center">
              <button onclick={handlePay} class="cursor-pointer bg-black text-white  px-5 py-1 rounded-full mt-3">Are you ready!</button>
            </div>
          {/if}
          
          
        </div>
        {:else}
          <div>
            <div class="mt-60">
              <p class="text-center text-4xl">Congratulations {payer}!</p>
              <div class="flex justify-center">
                <button onclick={handlePay} class="cursor-pointer bg-black text-white  px-5 py-1 rounded-full mt-3">Wanna play again?</button>
              </div>
            </div>
          </div>
      {/if}
  </div>
</div>

<p class="text-center fixed bottom-5 w-full text-gray-400">Developed by Abishek Ravichandran</p>