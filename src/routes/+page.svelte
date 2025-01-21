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

<main class="max-w-3xl mx-auto p-5">
    <h1 class="text-3xl font-bold text-slate-700 text-center mb-4">Chungmyung Hospital AI Assistant</h1>
    <p class="text-center text-slate-600 mb-4">Hello! I'm here to help answer your questions about our hospital. You can ask about:</p>
    
    <ul class="flex flex-wrap justify-center gap-2 mb-6">
        <li class="bg-blue-50 px-4 py-1.5 rounded-full text-sm text-slate-700">Hospital hours</li>
        <li class="bg-blue-50 px-4 py-1.5 rounded-full text-sm text-slate-700">Parking information</li>
        <li class="bg-blue-50 px-4 py-1.5 rounded-full text-sm text-slate-700">Appointment scheduling</li>
        <li class="bg-blue-50 px-4 py-1.5 rounded-full text-sm text-slate-700">Insurance coverage</li>
        <li class="bg-blue-50 px-4 py-1.5 rounded-full text-sm text-slate-700">COVID-19 policies</li>
        <li class="bg-blue-50 px-4 py-1.5 rounded-full text-sm text-slate-700">Visiting hours</li>
    </ul>

    <div class="h-[400px] overflow-y-auto border border-gray-200 rounded-lg p-5 bg-gray-50 mb-6">
        {#each messages as message}
            <div class="mb-3 {message.isUser ? 'ml-auto' : 'mr-auto'} max-w-[80%]">
                <div class="{message.isUser ? 
                    'bg-blue-500 text-white ml-auto' : 
                    'bg-blue-50 text-slate-700'} 
                    p-3 rounded-lg inline-block">
                    {message.text}
                </div>
            </div>
        {/each}
    </div>

    <form on:submit|preventDefault={handleSubmit} class="flex gap-3">
        <input 
            type="text" 
            bind:value={userInput} 
            placeholder="Type your question here..."
            class="flex-1 px-4 py-2 border border-gray-200 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
        >
        <button 
            type="submit" 
            class="px-6 py-2 bg-blue-500 text-white rounded-md hover:bg-blue-600 transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
        >
            Send
        </button>
    </form>
</main>

