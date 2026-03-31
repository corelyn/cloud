# 🟨📜 Usage for vanila JS

```javascript
// Minimal JS fetch example with system + user messages
async function getAIResponse(userPrompt) {
  try {
    const res = await fetch("https://corelyncloud-backend.onrender.com/chat/completions", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        apiKey: "YOUR_API_KEY", // Add your api key here
        model: "cerebras/llama3.1-8b", // Replace with your model
        messages: [
          { role: "system", content: "Your name is Corelyn" }, // system instruction
          { role: "user", content: userPrompt }                         // user input
        ]
      })
    });

    const data = await res.json();

    // Log full AI response
    console.log("AI Response:", data);

    // Return just the text of the first choice
    return data.choices?.[0]?.message?.content || data.text || data;

  } catch (err) {
    console.error("Error fetching AI response:", err);
    return null;
  }
}

// Example usage
getAIResponse("What is your name?").then(response => {
  console.log("Final Response:", response);
});
```