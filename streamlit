import streamlit as st
import pyodbc

def atualizar_status(usuario, acao):
    # criar conexão
    dados_conexao = (
        'Driver={SQL Server};'
        'Server=10.158.0.12;'  # Substitua pelo endereço IP do seu servidor
        'Database=UAU;'
        'UID=danilo.r;'  # Substitua pelo seu nome de usuário
        'PWD=ojt-ocbu-xiz;'    # Substitua pela sua senha
    )

    conexao = pyodbc.connect(dados_conexao)
    print('Conexão bem sucedida!')

    # criar cursor - executa os comandos
    cursor = conexao.cursor()

    # validar ação e executar o comando correspondente
    if acao == 'Ativar':
        comando_update = f"UPDATE Usuarios SET Status_usr = 0 WHERE Login_usr = '{usuario}'"
    elif acao == 'Inativar':
        comando_update = f"UPDATE Usuarios SET Status_usr = 1 WHERE Login_usr = '{usuario}'"
    else:
        return 'Ação inválida. Escolha "Ativar" ou "Inativar".'

    # executar comando UPDATE
    cursor.execute(comando_update)

    # realizar o commit para salvar as alterações no banco de dados
    conexao.commit()

    # fechar a conexão
    conexao.close()
    print('Conexão fechada.')

    return f'Operação bem sucedida para o usuário {usuario}.'

# criar interface Streamlit
st.title("Atualizar Status do Usuário")

# widgets
usuario = st.text_input("Nome do Usuário:")
acao = st.selectbox("Ação:", ['Ativar', 'Inativar'])

# botão para executar a ação
if st.button("Atualizar Status"):
    resultado = atualizar_status(usuario, acao)
    st.write(resultado)
