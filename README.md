from tkinter import *
from tkinter.filedialog import asksaveasfile, askopenfile

# Initialize the main window
root = Tk()
root.title("My Own Notepad")
root.geometry("600x500")

# Function to save the content of the text area into a file
def save_file():
    # Opens a dialog to save the file, defaulting to text files
    file_location = asksaveasfile(defaultextension=".txt", 
                                  filetypes=[("Text Documents", "*.txt"), ("All Files", "*.*")])
    if file_location is None:
        return
    # Get all text from the start ('1.0') to the end ('end')
    text_to_save = str(entry.get(1.0, END))
    file_location.write(text_to_save)
    file_location.close()

# Function to open a file and display its content in the text area
def open_file():
    # Opens a dialog to select and read a file
    file_location = askopenfile(mode='r', filetypes=[("Text Documents", "*.txt"), ("All Files", "*.*")])
    if file_location is not None:
        # Clear any existing text in the widget
        entry.delete(1.0, END)
        # Read content from the file
        content = file_location.read()
        # Insert content into the text area
        entry.insert(END, content)
        file_location.close()

# Top frame to house the Save and Open buttons
top_frame = Frame(root, bg="white")
top_frame.pack(side=TOP, fill=X)

# Button to trigger open_file functionality
open_button = Button(top_frame, text="Open", bg="white", command=open_file)
open_button.pack(side=LEFT, padx=5, pady=5)

# Button to trigger save_file functionality
save_button = Button(top_frame, text="Save", bg="white", command=save_file)
save_button.pack(side=LEFT, padx=5, pady=5)

# Button to exit the application
exit_button = Button(top_frame, text="Exit", bg="white", command=root.quit)
exit_button.pack(side=LEFT, padx=5, pady=5)

# Text widget where user can type out content
entry = Text(root, wrap=WORD, font=("Helvetica", 12))
entry.pack(fill=BOTH, expand=True, padx=5, pady=5)

# Start the Tkinter event loop
root.mainloop()
