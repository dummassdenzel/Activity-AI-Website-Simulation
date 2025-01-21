<script lang="ts">
    let messages: any = [];
    let userInput = '';
    
    // FAQ RESPONSES DITo
    const faqResponses = {
        'hours': 'Our hospital is open 24 hours a day, 7 days a week for emergencies. Regular outpatient services are available Monday-Friday from 8:00 AM to 6:00 PM.',
        'parking': 'Parking is available in the main garage on Level P1 and P2. The first 30 minutes are free, then $2/hour.',
        'appointment': 'To schedule an appointment, please call our main line at (555) 123-4567 or use our online patient portal.',
        'insurance': 'We accept most major insurance plans including Medicare and Medicaid. Please contact our billing department for specific coverage questions.',
        'covid': 'We offer COVID-19 testing and vaccination. Please wear a mask in all hospital areas. Screening is required at entrance.',
        'visiting': 'Visiting hours are from 10:00 AM to 8:00 PM daily. Two visitors per patient at a time.',
    };

    function handleSubmit() {
        if (!userInput.trim()) return;
        
        // ADD USR MESSAGES TO ARRY
        messages = [...messages, { text: userInput, isUser: true }];
        
        // DEFAULT RESPONSE
        let response = "I'm not sure about that. Please contact our front desk at (555) 123-4567 for more information.";
        
       
        const input = userInput.toLowerCase();
        if (input.includes('hour') || input.includes('open')) {
            response = faqResponses.hours;
        } else if (input.includes('park')) {
            response = faqResponses.parking;
        } else if (input.includes('appointment') || input.includes('schedule')) {
            response = faqResponses.appointment;
        } else if (input.includes('insurance') || input.includes('cover')) {
            response = faqResponses.insurance;
        } else if (input.includes('covid') || input.includes('test') || input.includes('vaccine')) {
            response = faqResponses.covid;
        } else if (input.includes('visit')) {
            response = faqResponses.visiting;
        }
        
        // ADD RESPONSES
        messages = [...messages, { text: response, isUser: false }];
        // RESET INPUT
        userInput = '';
    }
</script>

<main class="container">
    <h1>Chungmyung Hospital AI Assistant</h1>
    <p class="intro">Hello! I'm here to help answer your questions about our hospital. You can ask about:</p>
    <ul class="topics">
        <li>Hospital hours</li>
        <li>Parking information</li>
        <li>Appointment scheduling</li>
        <li>Insurance coverage</li>
        <li>COVID-19 policies</li>
        <li>Visiting hours</li>
    </ul>

    <div class="chat-container">
        {#each messages as message}
            <div class="message {message.isUser ? 'user' : 'bot'}">
                {message.text}
            </div>
        {/each}
    </div>

    <form on:submit|preventDefault={handleSubmit} class="input-form">
        <input 
            type="text" 
            bind:value={userInput} 
            placeholder="Type your question here..."
            class="input-field"
        >
        <button type="submit" class="send-button">Send</button>
    </form>
</main>

