<script>
// @ts-nocheck

    import confetti from "canvas-confetti";
    let user = $state("")
    let users = $state([])
    let payer = $state("")
    let resultOpposite = $state(true)

    const handleSubmit = (e) => {
        e.preventDefault()
        if (user) {
            users.push(user)
        }
        user = ""
    }

    const handleDelete = (index) => users.splice(index, 1)
    const fireConfetti = () => {
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
        if (!resultOpposite) {
            fireConfetti()
        }
    }
</script>

<main class="container">
  <div>
    <div>
      {#if resultOpposite}
        <div>
          <form onsubmit={handleSubmit} class="mb-3 mt-5">
            <label for="palname" class="form-label" >Enter pal's name</label>
            <input type="text" bind:value={user} class="form-control" id="palname"><br>
            <button class="btn btn-primary">Submit</button>
          </form>

          {#each users as user, index (index)}
            <div class="d-flex justify-content-between align-items-baseline">
              <p>{user}</p>
              <!-- svelte-ignore a11y_consider_explicit_label -->
              <button onclick={() => handleDelete(index)} class="btn border-0">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash-fill" viewBox="0 0 16 16">
                  <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5M8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5m3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0"/>
                </svg>
              </button>
            </div>
          {/each}

          {#if users.length > 1}
            <div class="d-flex justify-content-center">
              <button onclick={handlePay} class="btn btn-primary">Are you ready!</button>
            </div>
          {/if}
        </div>
      {:else}
        <div>
          <div class="d-flex flex-column justify-content-center align-items-center vh-100">
            <p class="d-inline-block">Congratulations {payer}!</p>
            <button onclick={handlePay} class="btn btn-primary">Wanna play again?</button>
          </div>
        </div>
      {/if}
    </div>
  </div>
</main>

<p class="fixed-bottom text-center">Developed by Abishek Ravichandran</p>