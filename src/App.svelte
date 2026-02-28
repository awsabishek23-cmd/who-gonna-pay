<script >
    import confetti from "canvas-confetti";
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
    const fireConfetti = () => {
    // First burst - center explosion
    confetti({
      particleCount: 120,
      spread: 80,
      origin: { y: 0.6 },
      gravity: 1.2,
      ticks: 500,
      colors: ['#ff0000', '#ffd700', '#00ff00', '#0000ff', '#ff69b4', '#ff8c00'],
      shapes: ['square', 'circle'],
      scalar: 1.2,
      drift: 0.1,
    })

    // Left cannon
    confetti({
      particleCount: 80,
      angle: 60,
      spread: 55,
      origin: { x: 0, y: 0.8 },
      gravity: 1.0,
      ticks: 600,
      colors: ['#26ccff', '#a25afd', '#ff5e7e', '#88ff5a', '#fcff42'],
      shapes: ['square', 'circle'],
      scalar: 1.4,
      drift: 0.5,
    })

    // Right cannon
    confetti({
      particleCount: 80,
      angle: 120,
      spread: 55,
      origin: { x: 1, y: 0.8 },
      gravity: 1.0,
      ticks: 600,
      colors: ['#26ccff', '#a25afd', '#ff5e7e', '#88ff5a', '#fcff42'],
      shapes: ['square', 'circle'],
      scalar: 1.4,
      drift: -0.5,
    })
}
    const handlePay = () => {
      payer = users[Math.round(Math.random() * (users.length - 1))]
      resultOpposite = !resultOpposite
      if(!resultOpposite){

        fireConfetti()
      }
    }
</script>

<div class="flex justify-center h-screen ">
  <div class="container max-w-5xl px-3 mt-9">
    <!-- svelte-ignore a11y_consider_explicit_label -->
      {#if resultOpposite}
        <div>
          <div>
            <p class="text-3xl pb-3">who gonna pay!</p>
          </div>
          <form onsubmit={handleSubmit}>
              <input type="text" bind:value={user} class="border-b-2 outline-none w-full text-2xl mb-2" placeholder="Enter a name"><br>
              <div class="flex justify-end-safe">
                <button class="cursor-pointer">
                  <p class="cursor-pointer bg-black text-white  px-5 py-1 rounded-full">Submit</p>
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