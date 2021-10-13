import sqlite3

con = sqlite3.connect('Registro_Programa.db')
cursor = con.cursor()

from tkinter import *

def presidenteCadastro():
    def salvarPresidente():
        cursor.execute(f"INSERT INTO Cadastro_Presidente VALUES ('{Entry3.get()}',{Entry4.get()},{Entry5.get()},{Entry6.get()})")
        con.commit()
        try:
            with open('Presidente_Cadastrado.txt', 'a') as arquivoUsuario:
                arquivoUsuario.write(Entry3.get() + '\n')
            with open('RG_Presidente.txt', 'a') as arquivoUsuario:
                arquivoUsuario.write(Entry4.get() + '\n')
            with open('cpf_Presidente.txt', 'a') as arquivoUsuario:
                arquivoUsuario.write(Entry5.get() + '\n')
            with open('senha_Presidente.txt', 'a') as arquivoUsuario:
                arquivoUsuario.write(Entry6.get() + '\n')
            programa2.destroy()
        except:
            print('Houve um erro!')


    programa2 = Tk()
    programa2.title('Cadastro')
    programa2.geometry('600x606+647+284')

    Frame1 = Frame(programa2)
    Frame1.place(relx=0.217, rely=0.132, relheight=0.668, relwidth=0.575)

    Entry3 = Entry(programa2)
    Entry3.place(relx=0.116, rely=0.152, height=20, relwidth=0.736)
    Entry4 = Entry(programa2)
    Entry4.place(relx=0.116, rely=0.294, height=20, relwidth=0.736)
    Entry5 = Entry(programa2)
    Entry5.place(relx=0.116, rely=0.456, height=20, relwidth=0.736)
    Entry6 = Entry(programa2, show='*')
    Entry6.place(relx=0.116, rely=0.618, height=20, relwidth=0.736)
    Label1 = Label(programa2)
    Label1.place(relx=0.116, rely=0.102, height=20, relwidth=0.736)
    Label1.configure(text='Nome do Presidente')
    Label2 = Label(programa2)
    Label2.place(relx=0.116, rely=0.244, height=20, relwidth=0.736)
    Label2.configure(text='RG')
    Label3 = Label(programa2)
    Label3.place(relx=0.116, rely=0.406, height=20, relwidth=0.736)
    Label3.configure(text='CPF')
    Label4 = Label(programa2)
    Label4.place(relx=0.116, rely=0.568, height=20, relwidth=0.736)
    Label4.configure(text='Senha')
    Button3 = Button(programa2, text='Cadastrar', command = salvarPresidente).place(relx=0.300, rely=0.730, height=60,relwidth=0.368)


    programa2.mainloop()

def cadastrar():
    def cadastroSecretaria():
        def salvarCadastro():
            cursor.execute(f"INSERT INTO Cadastro_Secretaria VALUES ('{Entry3.get()}',{Entry4.get()},{Entry5.get()},{Entry6.get()})")
            con.commit()
            try:
                with open('Secretaria_cadastradas.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry3.get() + '\n')
                with open('RG_secretaria.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry4.get() + '\n')
                with open('CPF_secretaria.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry5.get() + '\n')
                with open('senhas_secretaria.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry6.get() + '\n')
                programa2.destroy()
            except:
                print('houve um erro!')
        programa2 = Tk()
        programa2.title('Cadastro')
        programa2.geometry('600x606+647+284')

        Frame1 = Frame(programa2)
        Frame1.place(relx=0.217, rely=0.132, relheight=0.668, relwidth=0.575)

        Entry3 = Entry(programa2)
        Entry3.place(relx=0.116, rely=0.152, height=20, relwidth=0.736)
        Entry4 = Entry(programa2)
        Entry4.place(relx=0.116, rely=0.294, height=20, relwidth=0.736)
        Entry5 = Entry(programa2)
        Entry5.place(relx=0.116, rely=0.456, height=20, relwidth=0.736)
        Entry6 = Entry(programa2, show='*')
        Entry6.place(relx=0.116, rely=0.618, height=20, relwidth=0.736)
        Label1 = Label(programa2)
        Label1.place(relx=0.116, rely=0.102, height=20, relwidth=0.736)
        Label1.configure(text='Nome da secretaria')
        Label2 = Label(programa2)
        Label2.place(relx=0.116, rely=0.244, height=20, relwidth=0.736)
        Label2.configure(text='RG')
        Label3 = Label(programa2)
        Label3.place(relx=0.116, rely=0.406, height=20, relwidth=0.736)
        Label3.configure(text='CPF')
        Label4 = Label(programa2)
        Label4.place(relx=0.116, rely=0.568, height=20, relwidth=0.736)
        Label4.configure(text='Senha')
        Button3 = Button(programa2, text='Cad.Secretaria', command=salvarCadastro).place(relx=0.300, rely=0.730,height=60, relwidth=0.368)


    programa = Tk()
    programa.geometry("600x606+647+284")
    programa.title('Registro de Secretárias')


    Button2 = Button(programa,text='Cadastrar Secretarias', command=cadastroSecretaria).place(relx =0.300,rely=0.350,height= 80,width=250)
    programa.mainloop()



def loginPresidente():
    def verificaPresidente():
        with open('cpf_Presidente.txt', 'r') as arquivoUsuario:
            usuarios = arquivoUsuario.readlines()
        with open('senha_Presidente.txt', 'r') as arquivoUsuario:
            senhas = arquivoUsuario.readlines()
        usuarios = list(map(lambda x: x.replace('\n', ''), usuarios))
        senhas = list(map(lambda x: x.replace('\n', ''), senhas))
        usuario = Entry1.get()
        senha = Entry2.get()
        logado = False

        for i in range(len(usuarios)):
            if usuario == usuarios[i] and senha == senhas[i]:
                print('Usuário Logado')
                programa.destroy()
                logado = True

        if not logado:
            print('Usuario e/ou senha incorretos')
            programa.destroy()


    programa = Tk()
    programa.geometry("600x606+647+284")
    programa.title('Login do presidente')
    Label2 = Label(programa)
    Label2.place(relx=0.350, rely=0.200, height=80, relwidth=0.300)
    Label2.configure(text='CPF do Presidente')
    Label3 = Label(programa)
    Label3.place(relx=0.350, rely=0.400, height=80, relwidth=0.300)
    Label3.configure(text='Senha')
    Entry1 = Entry(programa)
    Entry1.place(relx=0.116, rely=0.332, height=20, relwidth=0.736)
    Entry2 = Entry(programa, show='*')
    Entry2.place(relx=0.116, rely=0.554, height=20, relwidth=0.736)



    Button1 = Button(programa,text='Login', command= verificaPresidente and cadastrar).place(relx =0.300,rely=0.823,height= 80,width=250)
    programa.mainloop()

def Pesquisadores():
    def cadastrarPesquisadores():
        def salvarCadastroPesq():
            cursor.execute(
                f"INSERT INTO Cadastro_Pesquisadores VALUES ('{Entry3.get()}',{Entry4.get()},{Entry5.get()},{Entry6.get()})")
            con.commit()
            try:
                with open('Pesquisadores_Cadastrados.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry3.get() + '\n')
                with open('RG_Pesquisadores.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry4.get() + '\n')
                with open('cpf_Pesquisadores.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry5.get() + '\n')
                with open('Pesquisadores_salvos.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry3.get() + '\n')
                with open('RG_salvo.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry4.get() + '\n')
                with open('cpf_salvo.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry5.get() + '\n')
                with open('senha_Pesquisadores.txt', 'a') as arquivoUsuario:
                    arquivoUsuario.write(Entry6.get() + '\n')

                programa2.destroy()

            except:
                print('houve um erro!')

        programa2 = Tk()
        programa2.title('Cadastro')
        programa2.geometry('600x606+647+284')

        Frame1 = Frame(programa2)
        Frame1.place(relx=0.217, rely=0.132, relheight=0.668, relwidth=0.575)

        Entry3 = Entry(programa2)
        Entry3.place(relx=0.116, rely=0.152, height=20, relwidth=0.736)
        Entry4 = Entry(programa2)
        Entry4.place(relx=0.116, rely=0.294, height=20, relwidth=0.736)
        Entry5 = Entry(programa2)
        Entry5.place(relx=0.116, rely=0.456, height=20, relwidth=0.736)
        Entry6 = Entry(programa2, show='*')
        Entry6.place(relx=0.116, rely=0.618, height=20, relwidth=0.736)
        Label1 = Label(programa2)
        Label1.place(relx=0.116, rely=0.102, height=20, relwidth=0.736)
        Label1.configure(text='Nome do Pesquisador')
        Label2 = Label(programa2)
        Label2.place(relx=0.116, rely=0.244, height=20, relwidth=0.736)
        Label2.configure(text='RG')
        Label3 = Label(programa2)
        Label3.place(relx=0.116, rely=0.406, height=20, relwidth=0.736)
        Label3.configure(text='CPF')
        Label4 = Label(programa2)
        Label4.place(relx=0.116, rely=0.568, height=20, relwidth=0.736)
        Label4.configure(text='Senha')
        Button3 = Button(programa2, text='Cadastrar', command=salvarCadastroPesq, ).place(relx=0.300, rely=0.730,
                                                                                          height=60, relwidth=0.368)

        programa2.mainloop()

    def escolherPesquisador():
        with open('Pesquisadores_Cadastrados.txt', 'r') as arquivoUsuario:
            pesquisadores = arquivoUsuario.readlines()
        pesquisador1 = pesquisadores[0]
        pesquisador2 = pesquisadores[1]
        pesquisador3 = pesquisadores[2]
        with open('RG_Pesquisadores.txt', 'r') as arquivoUsuario:
            rg = arquivoUsuario.readlines()
        rg1 = rg[0]
        rg2 = rg[1]
        rg3 = rg[2]
        with open('cpf_Pesquisadores.txt', 'r') as arquivoUsuario:
            cpf = arquivoUsuario.readlines()
        cpf1 = cpf[0]
        cpf2 = cpf[1]
        cpf3 = cpf[2]

        pesquisadores = list(map(lambda x: x.replace('\n', ''), pesquisadores))

        def funcEscolhido1():
            with open('Pesquisadores_Escolhidos.txt', 'a') as arquivoUsuario:
                arquivoUsuario.write(pesquisador1)

        def funcEscolhido2():
            with open('Pesquisadores_Escolhidos.txt', 'a') as arquivoUsuario:
                arquivoUsuario.write(pesquisador2)

        def funcEscolhido3():
            with open('Pesquisadores_Escolhidos.txt', 'a') as arquivoUsuario:
                arquivoUsuario.write(pesquisador3)


        def removerFunc():
            with open('Pesquisadores_Cadastrados.txt', 'w') as arquivoUsuario:
                ''
            with open('RG_Pesquisadores.txt', 'w') as arquivoUsuario:
                ''
            with open('cpf_Pesquisadores.txt', 'w') as arquivoUsuario:
                ''

        programa3 = Tk()
        programa3.geometry("600x620+647+284")
        programa3.title('Escolher Pesquisadores')

        Frame1 = Frame(programa3)
        Frame1.place(relx=0.217, rely=0.132, relheight=0.668, relwidth=0.575)
        Label1 = Label(programa3)
        Label1.place(relx=0.100, rely=0.162, height=40, relwidth=0.300)
        Label1.configure(text=pesquisador1)
        Label2 = Label(programa3)
        Label2.place(relx=0.100, rely=0.380, height=40, relwidth=0.300)
        Label2.configure(text=pesquisador2)
        Label3 = Label(programa3)
        Label3.place(relx=0.100, rely=0.622, height=40, relwidth=0.300)
        Label3.configure(text=pesquisador3)
        Label5 = Label(programa3)
        Label5.place(relx=0.410, rely=0.162, height=40, relwidth=0.220)
        Label5.configure(text=rg1)
        Label6 = Label(programa3)
        Label6.place(relx=0.410, rely=0.380, height=40, relwidth=0.220)
        Label6.configure(text=rg2)
        Label7 = Label(programa3)
        Label7.place(relx=0.410, rely=0.622, height=40, relwidth=0.220)
        Label7.configure(text=rg3)
        Label5 = Label(programa3)
        Label5.place(relx=0.600, rely=0.162, height=40, relwidth=0.300)
        Label5.configure(text=cpf1)
        Label6 = Label(programa3)
        Label6.place(relx=0.600, rely=0.380, height=40, relwidth=0.300)
        Label6.configure(text=cpf2)
        Label7 = Label(programa3)
        Label7.place(relx=0.600, rely=0.622, height=40, relwidth=0.300)
        Label7.configure(text=cpf3)
        Label1 = Label(programa3)
        Label1.place(relx=0.100, rely=0.100, height=40, relwidth=0.300)
        Label1.configure(text='NOME:')
        Label2 = Label(programa3)
        Label2.place(relx=0.360, rely=0.100, height=40, relwidth=0.300)
        Label2.configure(text='RG:')
        Label3 = Label(programa3)
        Label3.place(relx=0.560, rely=0.100, height=40, relwidth=0.300)
        Label3.configure(text='CPF:')
        Button1 = Button(programa3, text='Aprovar', command=funcEscolhido1).place(relx=0.330, rely=0.213, height=40,
                                                                                  width=200)
        Button2 = Button(programa3, text='Aprovar', command=funcEscolhido2).place(relx=0.330, rely=0.453, height=40,
                                                                                  width=200)
        Button3 = Button(programa3, text='Aprovar', command=funcEscolhido3).place(relx=0.330, rely=0.713, height=40,
                                                                                  width=200)
        Button6 = Button(programa3, text='Remover', command=removerFunc).place(relx=0.330, rely=0.873, height=60,
                                                                               width=200)
    programa = Tk()
    programa.geometry("600x606+647+284")
    programa.title('Registro de Pesquisadores')

    Frame1 = Frame(programa)
    Frame1.place(relx=0.217, rely=0.132, relheight=0.668, relwidth=0.575)

    Button1 = Button(programa,text='Cadastrar Pesquisador', command=cadastrarPesquisadores).place(relx=0.300, rely=0.223,height=80, width=250)
    Button2 = Button(programa,text='Escolher Pesquisador', command=escolherPesquisador).place(relx=0.300, rely=0.523,height=80, width=250)
    programa.mainloop()

def loginSecretaria():
    def verificaSecretaria():
        with open('Secretaria_cadastradas.txt', 'r') as arquivoUsuario:
            usuarios = arquivoUsuario.readlines()
        with open('senhas_secretaria.txt', 'r') as arquivoUsuario:
            senhas = arquivoUsuario.readlines()
        usuarios = list(map(lambda x: x.replace('\n', ''), usuarios))
        senhas = list(map(lambda x: x.replace('\n', ''), senhas))
        usuario = Entry1.get()
        senha = Entry2.get()
        logado = False

        for i in range(len(usuarios)):
            if usuario == usuarios[i] and senha == senhas[i]:
                print('Usuário Logado')
                programa.destroy()
                logado = True
        if not logado:
            print('Usuario e/ou senha incorretos')
            programa.destroy()
    programa = Tk()
    programa.geometry("600x606+647+284")
    programa.title('Login da Secretaria')
    Label2 = Label(programa)
    Label2.place(relx=0.350, rely=0.200, height=80, relwidth=0.300)
    Label2.configure(text='CPF da Secretaria')
    Label3 = Label(programa)
    Label3.place(relx=0.350, rely=0.400, height=80, relwidth=0.300)
    Label3.configure(text='Senha')
    Entry1 = Entry(programa)
    Entry1.place(relx=0.116, rely=0.332, height=20, relwidth=0.736)
    Entry2 = Entry(programa, show='*')
    Entry2.place(relx=0.116, rely=0.554, height=20, relwidth=0.736)

    Button1 = Button(programa, text='Login', command=verificaSecretaria and Pesquisadores).place(relx=0.300, rely=0.823,height=80, width=250)

    programa.mainloop()

programa = Tk()
programa.geometry("600x606+647+284")
programa.title('Tela inicial')

Frame1 = Frame(programa)
Frame1.place(relx =0.217,rely=0.132,relheight= 0.668,relwidth=0.575)

Label1 = Label(Frame1)
Label1.place(relx =0.377,rely=0.179,height= 60,width=80)
Label1.configure(text = 'Usuário(CPF)')

Button1 = Button( text='Cadastrar Presidente', command = presidenteCadastro).place(relx =0.300,rely=0.223,height= 80,width=250)
Button2 = Button( text='Login do Presidente',command = loginPresidente).place(relx =0.300,rely=0.423,height= 80,width=250)
Button3 = Button( text='Login Secretária',command = loginSecretaria).place(relx =0.300,rely=0.623,height= 80,width=250)
programa.mainloop()
