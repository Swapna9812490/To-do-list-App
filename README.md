import streamlit as st

st.set_page_config(page_title="AI-Powered To-Do List", page_icon="✅")

st.title("📝 AI-Powered To-Do List")

# Session state for tasks
if "tasks" not in st.session_state:
    st.session_state.tasks = []

# Add new task
new_task = st.text_input("Enter a task")
if st.button("➕ Add Task"):
    if new_task.strip():
        st.session_state.tasks.append({"task": new_task, "done": False})

# Show tasks
st.subheader("Your Tasks")
for i, t in enumerate(st.session_state.tasks):
    checked = st.checkbox(t["task"], value=t["done"], key=f"task_{i}")
    st.session_state.tasks[i]["done"] = checked

# Remove completed
if st.button("🗑 Remove Completed"):
    st.session_state.tasks = [t for t in st.session_state.tasks if not t["done"]]

# Clear all
if st.button("❌ Clear All"):
    st.session_state.tasks = []
