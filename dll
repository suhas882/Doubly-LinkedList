import tkinter as tk
from tkinter import messagebox
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None
class DoublyLinkedList:
    def __init__(self):  # FIXED: Changed from `_init_` to `__init__`
        self.head = None
    def push(self, data):
        new_node = Node(data)
        new_node.next = self.head
        if self.head:
            self.head.prev = new_node
        self.head = new_node
    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        last = self.head
        while last.next:
            last = last.next
        last.next = new_node
        new_node.prev = last
    def insert_at_position(self, data, position):
        new_node = Node(data)
        if position <= 0:  
            self.push(data)
            return  
        current = self.head
        index = 0
        while current and index < position:
            current = current.next
            index += 1
        if current is None:  
            self.append(data)
        else:
            new_node.next = current
            new_node.prev = current.prev
            current.prev = new_node
            if new_node.prev:  
                new_node.prev.next = new_node
            else:  
                self.head = new_node
    def delete_first(self):
        if self.head:
            self.head = self.head.next
            if self.head:
                self.head.prev = None
    def delete_last(self):
        if not self.head:
            return
        last = self.head
        while last.next:
            last = last.next
        if last.prev:
            last.prev.next = None
        else:
            self.head = None
    def print_list(self, direction):
        node = self.head
        values = []
        if direction == "forward":
            while node:
                values.append(str(node.data))
                node = node.next
        else:  
            while node and node.next:
                node = node.next
            while node:
                values.append(str(node.data))
                node = node.prev
        return values
class App:
    def __init__(self, root):  # FIXED: Changed `_init_` to `__init__`
        self.root = root
        self.root.title("Doubly Linked List GUI")
        self.heading = tk.Label(root, text="Doubly Linked List Manager", font=("Helvetica", 18, "bold"))
        self.heading.pack(pady=10)
        self.dll = DoublyLinkedList()
        self.canvas = tk.Canvas(root, height=150, width=700, bg="white")
        self.canvas.pack(pady=20)
        self.wrapper_frame = tk.Frame(root)
        self.wrapper_frame.pack()
        self.insert_frame = tk.Frame(self.wrapper_frame)
        self.insert_frame.pack(side=tk.LEFT, padx=10)
        self.label = tk.Label(self.insert_frame, text="Insertions:", font=("Helvetica", 14))
        self.label.pack(pady=5)
        self.entry = tk.Entry(self.insert_frame, font=("Helvetica", 12))
        self.entry.pack(pady=5)
        self.push_button = tk.Button(self.insert_frame, text="Insert at Beginning", font=("Helvetica", 12), command=self.push)
        self.push_button.pack(pady=5)
        self.append_button = tk.Button(self.insert_frame, text="Insert at End", font=("Helvetica", 12), command=self.append)
        self.append_button.pack(pady=5)
        self.middle_frame = tk.Frame(self.wrapper_frame)
        self.middle_frame.pack(side=tk.LEFT, padx=20)
        self.position_label = tk.Label(self.middle_frame, text="Position Insert/Delete:", font=("Helvetica", 14))
        self.position_label.pack(pady=5)
        self.position_entry = tk.Entry(self.middle_frame, font=("Helvetica", 12))
        self.position_entry.pack(pady=5)
        self.insert_button = tk.Button(self.middle_frame, text="Insert at Position", font=("Helvetica", 12), command=self.insert_at_position)
        self.insert_button.pack(pady=5)
        self.print_forward_button = tk.Button(self.middle_frame, text="Print Forward", font=("Helvetica", 12), command=self.print_forward)
        self.print_forward_button.pack(pady=5)
        self.print_backward_button = tk.Button(self.middle_frame, text="Print Backward", font=("Helvetica", 12), command=self.print_backward)
        self.print_backward_button.pack(pady=5)
        self.delete_frame = tk.Frame(self.wrapper_frame)
        self.delete_frame.pack(side=tk.LEFT, padx=10)
        self.label_delete = tk.Label(self.delete_frame, text="Deletions:", font=("Helvetica", 14))
        self.label_delete.pack(pady=5)
        self.delete_first_button = tk.Button(self.delete_frame, text="Delete from Beginning", font=("Helvetica", 12), command=self.delete_first)
        self.delete_first_button.pack(pady=5)
        self.delete_last_button = tk.Button(self.delete_frame, text="Delete from End", font=("Helvetica", 12), command=self.delete_last)
        self.delete_last_button.pack(pady=5)
    def push(self):
        data = self.get_entry_data()
        if data is not None:
            self.dll.push(data)
            self.show_message("Inserted at beginning.")
            self.draw_list()
    def append(self):
        data = self.get_entry_data()
        if data is not None:
            self.dll.append(data)
            self.show_message("Inserted at end.")
            self.draw_list()
    def insert_at_position(self):
        data = self.get_entry_data()
        position = self.get_position_data()
        if data is not None and position is not None:
            self.dll.insert_at_position(data, position)
            self.show_message(f"Inserted {data} at position {position}.")
            self.draw_list()
    def delete_first(self):
        self.dll.delete_first()
        self.show_message("Deleted from beginning.")
        self.draw_list()
    def delete_last(self):
        self.dll.delete_last()
        self.show_message("Deleted from end.")
        self.draw_list()
    def print_forward(self):
        values = self.dll.print_list("forward")
        self.show_result(values)
    def print_backward(self):
        values = self.dll.print_list("backward")
        self.show_result(values)
    def get_entry_data(self):
        try:
            data = int(self.entry.get())
            self.entry.delete(0, tk.END)
            return data
        except ValueError:
            messagebox.showerror("Input error", "Please enter a valid integer.")
            return None
    def get_position_data(self):
        try:
            position = int(self.position_entry.get())
            self.position_entry.delete(0, tk.END)
            return position
        except ValueError:
            messagebox.showerror("Input error", "Please enter a valid position.")
            return None
    def show_message(self, message):
        messagebox.showinfo("Info", message)
    def show_result(self, values):
        self.canvas.delete("all")
        if values:
            self.canvas.create_text(350, 75, text=" <-> ".join(values), font=("Helvetica", 16))
        else:
            self.canvas.create_text(350, 75, text="List is empty.", font=("Helvetica", 16))
if __name__ == "__main__":  # FIXED: Corrected `_main_` to `__main__`
    root = tk.Tk()
    app = App(root)
    root.mainloop()
