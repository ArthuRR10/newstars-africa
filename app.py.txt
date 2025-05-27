from flask import Flask, jsonify
from threading import Thread
import random

app = Flask(__name__)

nomes = [
    "Kwame", "Amina", "Thabo", "Zola", "Kofi", "Amara", "Jelani", "Nia",
    "Obasi", "Ifunanya", "Bakari", "Ayana", "Simba", "Sibongile", "Chinedu", "Eshe",
    "Masego", "Omari", "Zuberi", "Ngozi", "Tendai", "Ife", "Jabari", "Makena",
    "Sekou", "Halima", "Lerato", "Chika", "Ayodele", "Naledi", "Abena", "Mpilo",
    "Baraka", "Kehinde", "Neema", "Tumelo", "Yaw", "Fatou", "Amogelang", "Zanele"
]

sobrenomes = [
    "Okafor", "Mensah", "Diallo", "Ndlovu", "Abebe", "Mwangi", "Tshabalala", "Kamara",
    "Afolayan", "Ngoma", "Balewa", "Achebe", "Onyango", "Dlamini", "Kouyaté", "Mbatha",
    "Obeng", "Jalloh", "Achieng", "Adesina", "Makonnen", "Mugabe", "Maponya", "Chikere",
    "Ndour", "Eze", "Mandela", "Nkosi", "Banda", "Otieno", "Sekibo", "Sankara",
    "Molapo", "Agyeman", "Molefe", "Odinga", "Shabangu", "Bakayoko", "Diouf", "Nkrumah"
]

nacionalidades = [
    ("🇳🇬 Nigéria", 4), ("🇸🇳 Senegal", 3), ("🇨🇮 Costa do Marfim", 3), ("🇿🇦 África do Sul", 3),
    ("🇬🇭 Gana", 3), ("🇨🇲 Camarões", 2), ("🇲🇱 Mali", 2), ("🇩🇿 Argélia", 2),
    ("🇲🇦 Marrocos", 2), ("🇹🇳 Tunísia", 2), ("🇬🇳 Guiné", 1), ("🇨🇩 Congo", 1),
    ("🇺🇬 Uganda", 1), ("🇪🇹 Etiópia", 1), ("🇿🇲 Zâmbia", 1)
]

posicoes = [
    "Goleiro", "Zagueiro", "Lateral Direito", "Lateral Esquerdo", "Volante",
    "Meia Central", "Meia Ofensivo", "Ponta Direita", "Ponta Esquerda", "Centroavante"
]

comparacoes = [
    "Victor Osimhen", "Sadio Mané", "Mohamed Salah", "Achraf Hakimi", "Thomas Partey",
    "André Onana", "Wilfried Zaha", "Kalidou Koulibaly", "Franck Kessié", "Yassine Bounou",
    "Youssef En-Nesyri", "Eric Bailly", "Riyad Mahrez", "Taiwo Awoniyi", "Ismaila Sarr"
]

capacidade_atual = [
    "Reserva na National League", "Titular na National League", "Reserva na League Two", 
    "Titular na League Two", "Reserva na League One", "Titular na League One"
]

capacidade_potencial = [
    "Reserva na League Two", "Titular na League Two", "Reserva na League One", 
    "Titular na League One", "Reserva na Championship", "Reserva na NLEDF", 
    "Titular na Championship", "Titular na NLEDF"
]

# Aumentando as chances de 4 e 5 estrelas
estrelas_pesos = [(2, 10), (3, 20), (4, 45), (5, 25)]

@app.route('/')
def gerar_jogador():
    nome = f"{random.choice(nomes)} {random.choice(sobrenomes)}"
    nacionalidade = random.choices(nacionalidades, weights=[n[1] for n in nacionalidades])[0][0]
    posicao = random.choice(posicoes)
    comparacao = random.choice(comparacoes)
    atual = random.choice(capacidade_atual)
    potencial = random.choice(capacidade_potencial)
    estrelas = random.choices([e[0] for e in estrelas_pesos], weights=[e[1] for e in estrelas_pesos])[0]
    estrelas_txt = "<:sstar:1214063700886036532>" * estrelas

    return jsonify({
        "nome": nome,
        "nacionalidade": nacionalidade,
        "posicao": posicao,
        "comparacao": comparacao,
        "cap_atual": atual,
        "cap_potencial": potencial,
        "estrelas": estrelas_txt 
    })

def run():
    app.run(host='0.0.0.0', port=8080)

Thread(target=run).start()
