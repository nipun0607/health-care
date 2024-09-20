<script>
    // Service list data
    let services = [
        { id: 1, name: 'Consultation', description: 'General health checkup', price: 50 },
        { id: 2, name: 'X-Ray', description: 'Full body scan', price: 100 },
    ];

    let newService = { name: '', description: '', price: '' };
    let editIndex = null;  // To track the index of the service being edited

    // Add new service function
    const addService = () => {
        if (newService.name && newService.description && newService.price) {
            services = [...services, { ...newService, id: services.length + 1 }];
            newService = { name: '', description: '', price: '' }; // Clear the form
        }
    };

    // Delete service function
    const deleteService = (index) => {
        services = services.filter((_, i) => i !== index);
    };

    // Update service function
    const editService = (index) => {
        newService = { ...services[index] }; // Load the service to the form for editing
        editIndex = index;
    };

    const updateService = () => {
        if (editIndex !== null) {
            services[editIndex] = { ...newService };
            newService = { name: '', description: '', price: '' }; // Clear the form
            editIndex = null; // Exit edit mode
        }
    };
</script>

<!-- List of Services -->
<h2>Healthcare Services</h2>
<ul>
    {#each services as service, index}
        <li>
            <strong>{service.name}</strong>: {service.description} - ${service.price}
            <button on:click={() => editService(index)}>Edit</button>
            <button on:click={() => deleteService(index)}>Delete</button>
        </li>
    {/each}
</ul>

<!-- Form to Add/Edit Service -->
<h3>{editIndex !== null ? 'Edit' : 'Add'} Service</h3>
<form on:submit|preventDefault={editIndex !== null ? updateService : addService}>
    <label>Name</label>
    <input type="text" bind:value={newService.name} required />

    <label>Description</label>
    <input type="text" bind:value={newService.description} required />

    <label>Price ($)</label>
    <input type="number" bind:value={newService.price} required />

    <button type="submit">{editIndex !== null ? 'Update' : 'Add'} Service</button>
</form>
<style>
    h2, h3 {
        font-family: Arial, sans-serif;
        color: #333;
    }

    form {
        margin: 20px 0;
        display: flex;
        flex-direction: column;
    }

    label {
        margin: 5px 0;
    }

    input {
        padding: 5px;
        margin-bottom: 10px;
        border: 1px solid #ccc;
        border-radius: 4px;
    }

    button {
        padding: 10px 15px;
        background-color: #007BFF;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }

    button:hover {
        background-color: #0056b3;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        margin: 10px 0;
        padding: 10px;
        background-color: #f9f9f9;
        border: 1px solid #ccc;
        border-radius: 4px;
    }

    li button {
        margin-left: 10px;
        background-color: #FF4136;
    }

    li button:first-child {
        background-color: #2ECC40;
    }
</style>
