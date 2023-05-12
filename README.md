# potential-waffle
Para fazer login na Vivo utilizando Python
import requests

# URL da página de login da Vivo
url = 'https://login.vivo.com.br/loginmarca/appmanager/marca/publico'

# Dados de login
username = 'seu_username'
password = 'sua_senha'

# Cria um objeto de sessão
session = requests.Session()

# Envia uma solicitação GET para a página de login da Vivo para obter o cookie de sessão
response = session.get(url)

# Extrai o valor do parâmetro "javax.faces.ViewState" do HTML da página de login
viewstate = response.text.split('javax.faces.ViewState" value="')[1].split('"')[0]

# Envia uma solicitação POST com os dados de login
response = session.post(url, data={
    'formlogin': 'formlogin',
    'username': username,
    'password': password,
    'javax.faces.ViewState': viewstate,
    'javax.faces.source': 'botaoLogar',
    'javax.faces.partial.event': 'click',
    'javax.faces.partial.execute': 'botaoLogar formlogin',
    'javax.faces.partial.render': 'formlogin',
    'botaoLogar': 'botaoLogar'
})

# Verifica se o login foi bem-sucedido
if 'Bem-vindo' in response.text:
    print('Login bem-sucedido!')
else:
    print('Login falhou.')
