import tkinter as tk
from tkinter import ttk
from tkinter import messagebox


# Функция для добавления нового студента
def add_student():
    # Открываем новое окно для ввода данных
    def save_data():
        name = entry_name.get().strip()
        age = entry_age.get().strip()
        skills = entry_skills.get().strip()

        if not all([name, age, skills]):
            messagebox.showerror(title="Ошибка!", message="Поля не должны быть пустыми!")
            return

        try:
            age = int(entry_age.get())
        except ValueError:
            messagebox.showerror(title="Ошибка!", message="Возраст должен быть числом!")
            return

        tree.insert("", tk.END, values=(name, age, skills))
        window.destroy()


    window = tk.Toplevel(root)
    window.title("Добавить студента")
    window.geometry(f"+{(window.winfo_screenwidth() // 2) - 150}+{(window.winfo_screenheight() // 2) - 75}")

    label_name = tk.Label(window, text="Имя:")
    label_name.grid(row=0, column=0, padx=10, pady=5)
    entry_name = tk.Entry(window)
    entry_name.grid(row=0, column=1, padx=10, pady=5)

    label_age = tk.Label(window, text="Возраст:")
    label_age.grid(row=1, column=0, padx=10, pady=5)
    entry_age = tk.Entry(window)
    entry_age.grid(row=1, column=1, padx=10, pady=5)

    label_skills = tk.Label(window, text="Навыки:")
    label_skills.grid(row=2, column=0, padx=10, pady=5)
    entry_skills = tk.Entry(window)
    entry_skills.grid(row=2, column=1, padx=10, pady=5)

    button_save = tk.Button(window, text="Сохранить", command=save_data)
    button_save.grid(row=3, columnspan=2, padx=10, pady=5)


# Функция для удаления выбранного студента
def delete_student():
    selected_item = tree.focus()
    if selected_item:
        tree.delete(selected_item)
    else:
        messagebox.showwarning(title="Предупреждение!", message="Выберите студента для удаления.")


# Основная программа
root = tk.Tk()
root.title("IT_Exel.COM")
root.geometry("700x400")
root.geometry(f"+{(root.winfo_screenwidth() // 2) - 350}+{(root.winfo_screenheight() // 2) - 200}")

# Кнопки управления
btn = ttk.Button(text="Добавить ученика", command=add_student)
btn.pack()
btn = ttk.Button(text="Удалить", command=delete_student)
btn.pack()

# Дерево для отображения данных
columns = ("Имя", "Возраст", "Навыки")
tree = ttk.Treeview(columns=columns, show="headings")
tree.pack(fill=tk.BOTH, expand=1)

for col in columns:
    tree.heading(col, text=col)

# Запуск основного цикла
root.mainloop()
