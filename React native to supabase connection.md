# How to avoid hardcoded credentials in react native app 
(bcuz if we keep .env file inside the app, attacker
can decompile and see the hardcoded credentials)

## instead of using supabase directly on react native app, there are 2 ways. 

* Proxy server (using express.    backend)
* Supabase edge functions 


# How supabase edge functions works?

Yeah, I understand. How edge functions actually work. 
I need to create separate project for supabase. 
Where I write down the edge functions and then deploy it to supabase. 
After that I call those edge functions from app, right?

Exactly! You've got it 100% correct! 🎯

Let me confirm your understanding with a clear visual flow:

📁 Project Structure

```
Your Computer (Development)
├── 📱 React Native App Project/
│   ├── App.js
│   ├── lib/
│   │   └── supabase-client.js  (calls edge functions)
│   └── package.json
│
└── 🔧 Supabase Backend Project/  (SEPARATE folder!)
    ├── supabase/
    │   └── functions/
    │       ├── get-instruments/
    │       │   └── index.ts
    │       └── create-order/
    │           └── index.ts
    └── supabase.json
```

🔄 The Complete Flow

Step 1: Create Supabase Backend Project

```bash
# In a separate folder (not your app folder)
mkdir my-supabase-backend
cd my-supabase-backend

# Initialize Supabase
supabase init
```

Step 2: Write Edge Functions

```typescript
// supabase/functions/get-instruments/index.ts
export const handler = async (req: Request) => {
  // Server-side code here
  const supabase = createClient(
    Deno.env.get("SUPABASE_URL")!,
    Deno.env.get("SUPABASE_SERVICE_ROLE_KEY")! // Secure!
  );
  
  const { data } = await supabase.from('instruments').select('*');
  return new Response(JSON.stringify({ data }));
};
```

Step 3: Deploy to Supabase Cloud

```bash
# Deploy the function to Supabase's servers
supabase functions deploy get-instruments

# Now it lives at:
# https://[your-project-id].supabase.co/functions/v1/get-instruments
```

Step 4: Call from Your React Native App

```typescript
// In your React Native App project
import { supabase } from './lib/supabase-client';

const fetchInstruments = async () => {
  // This calls the deployed edge function
  const { data, error } = await supabase.functions.invoke('get-instruments');
  console.log(data); // Data from your Supabase database
};
```

🎯 Key Points to Remember

Aspect Location Purpose
Edge Function Code Your local supabase-backend folder Where you write the logic
Edge Function Runtime Supabase Cloud Servers Where the code actually executes
Your App User's device Calls the function via HTTP
Database Supabase Cloud Accessed securely by the function

✅ Checklist for Your Workflow

· Create two separate folders on your computer
· Write edge functions in the supabase-backend folder
· Deploy functions using Supabase CLI
· In your app, use supabase.functions.invoke() to call them
· Never expose service_role key in your app

---

You nailed it! This separation keeps your sensitive keys safe on the server while your app just makes simple HTTP calls. 🚀

Need help with the actual deployment commands or writing your first edge function?
