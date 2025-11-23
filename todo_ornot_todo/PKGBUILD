pkgname=todo_ornot_todo
pkgver=1.2
pkgrel=1
pkgdesc="simple todo list"
arch=('x86_64')
license=('custom')
depends=()
source=('https://raw.githubusercontent.com/SuperBome/CLI-todo-list/refs/heads/main/todo_ornot_todo.cpp'
        'https://raw.githubusercontent.com/SuperBome/CLI-todo-list/refs/heads/main/todolist.txt')
md5sums=('1d74162920dd1c0dd09347bd8816e372'
         '59d9fb1ff0496cb2ad20ffb32378bea5')

build()
{
    cd "$srcdir"
    g++ todo_ornot_todo.cpp -o td_on_td
}

package()
{
    install -Dm755 "$srcdir/td_on_td" "$pkgdir/usr/bin/td_on_td"

    install -Dm644 "$srcdir/todolist.txt" "$pkgdir/usr/share/todo_ornot_todo/todolist.txt"
}
