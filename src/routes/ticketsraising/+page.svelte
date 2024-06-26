<script>
    import { onMount } from 'svelte';
    import axios from 'axios';

    let title = '';
    let description = '';
    let status = 'Open';
    let message = '';

    // Function to create a new ticket
    async function createTicket() {
        try {
            const response = await axios.post('http://localhost:3000/tickets', {
                title,
                description,
                status
            });
            console.log('Ticket created successfully:', response.data);
            message = 'Ticket created successfully';
            title = '';
            description = '';
        } catch (error) {
            console.error('Error creating ticket:', error);
            message = 'Error creating ticket';
        }
    }
</script>
<body>
<h1>CREATE TICKET</h1>

<form on:submit|preventDefault={createTicket}>
    <div>
        <label for="title">Title</label>
        <input type="text" id="title" bind:value={title} required />
    </div>
    <div>
        <label for="description">Description</label>
        <textarea id="description" bind:value={description} required></textarea>
    </div>
    <a href="http://localhost:5173/ticketslisting"><button type ="submit">Create Ticket</button></a>
</form>

{#if message}
    <p>{message}</p>
{/if}

<style>

    body{
        align-items:center;
    }

    h1 {
        color: #333;
        text-align: center;
        margin-top: 20px;
    }

    form {
        background: white;
        padding: 10px;
        margin-left:400px;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        max-width: 600px;
        width: 100%;
        margin-bottom: 30px;
        
        }

    form div {
        margin-bottom: 10px;
    }

    label {
        display: block;
        margin-bottom: 5px;
        font-weight: bold;
        color: #07BFF;
    }

    input, textarea {
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        margin-bottom: 10px;
    }

    button {
        width: 100%;
        padding: 10px;
        background-color: #007BFF;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 16px;
    }

    button:hover {
        background-color: orange;
    }

    p {
        color: #07BFF;
        text-align: center;
        font-weight: bold;
    }
</style>


</body>