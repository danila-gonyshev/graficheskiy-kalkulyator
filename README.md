import tkinter as tk


class Calculator:
    def __init__(self, master):
        self.master = master
        self.master.title("Calculator")
        self.master.geometry("360x410")

        self.result_var = tk.StringVar()

        self.entry = tk.Entry(
            master,
            textvariable=self.result_var,
            font=("Helvetica", 20),
            bd=15,
            insertwidth=4,
            width=14,
            justify="right",
        )
        self.entry.grid(row=0, column=0, columnspan=4)

        button_texts = [
            ("7", 1, 0),
            ("8", 1, 1),
            ("9", 1, 2),
            ("/", 1, 3),
            ("4", 2, 0),
            ("5", 2, 1),
            ("6", 2, 2),
            ("*", 2, 3),
            ("1", 3, 0),
            ("2", 3, 1),
            ("3", 3, 2),
            ("-", 3, 3),
            ("0", 4, 0),
            ("C", 4, 1),
            ("=", 4, 2),
            ("+", 4, 3),
        ]

        for text, row, column in button_texts:
            button = tk.Button(
                master,
                text=text,
                font=("Helvetica", 20),
                height=2,
                width=5,
                command=lambda t=text: self.button_click(t),
            )
            button.grid(row=row, column=column)

    def button_click(self, text):
        if text == "=":
            try:
                result = int(eval(self.result_var.get()))
                self.result_var.set(result)
            except Exception as e:
                self.result_var.set("Error")
        elif text == "C":
            self.result_var.set("")
        else:
            current_text = self.result_var.get()
            current_text += text
            self.result_var.set(current_text)


if __name__ == "__main__":
    root = tk.Tk()
    calculator = Calculator(root)
    root.mainloop()
