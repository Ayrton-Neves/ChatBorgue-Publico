import streamlit as st
import google.generativeai as genai

st.set_page_config(page_title='ChatBorgue', page_icon='🤖')
st.page_link("https://github.com/Ayrton-Neves/ChatBorgue/blob/main/ChatBorgue.py", label="Código GitHub", icon="🔗")
st.title('🤖 ChatBorgue')

genai.configure(api_key="USER_KEY")

# Set up the model
generation_config = {
  "temperature": 0.9,
  "top_p": 1,
  "top_k": 1,
  "max_output_tokens": 2048,
}

safety_settings = [
  {
    "category": "HARM_CATEGORY_HARASSMENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_HATE_SPEECH",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
]

model = genai.GenerativeModel(model_name="gemini-1.0-pro",
                              generation_config=generation_config,
                              safety_settings=safety_settings)

convo = model.start_chat(history=[
  {
    "role": "user",
    "parts": ["Você é o ChatBorgue, um chatbot ia para exercícios e práticas saudáveis feitas em casa, você é integro, confiável e respeitável, portanto não passa informações falsas ou inventadas, caso não consiga responder uma pergunta, você não inventa e diz que não sabe ou pede para refazer a pergunta. Como seu foco é em exercícios e práticas saudáveis, você responde tópicos diferentes com a seguinte frase “Desculpe, eu sou um chatbot de exercícios e práticas saudáveis em casa, e não respondo questões de outros assuntos, espero que compreenda. 😊”. Quando você for informado sobre algum tipo de impedimento físico complicado, por exemplo: sem uma perna ou braço, problemas de junta e etc, deve retornar a seguinte frase “Para sua segurança e saúde, recomendo procurar um especialista formado. 📖”. Você sempre tenta responder as perguntas feitas a você de forma amigável e simpática e se preocupa com o bem estar da outra pessoa."]
  },
  {
    "role": "model",
    "parts": ["OK. 😊"]
  },
])

# Initialize chat history
if 'messages' not in st.session_state:
    st.session_state.messages = []

# Display chat messages from history on app rerun
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# React to user input
if prompt := st.chat_input("Faça uma pergunta:", key=5472):
    # Display user message in chat message container
    with st.chat_message("user"):
        convo.send_message(prompt)
        st.markdown(prompt)
    # Add user message to chat history
    st.session_state.messages.append({"role": "user", "content": prompt})

    resposta = convo.last.text
    # Display assistant response in chat message container
    with st.chat_message("ai"):
        st.markdown(resposta)
    # Add assistant response to chat history
    st.session_state.messages.append({"role": "ai", "content": resposta})
