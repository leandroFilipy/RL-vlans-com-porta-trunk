# RL - VLANs com Porta Trunk 🚦🔌

Bem-vindo(a)! Este repositório contém exemplos e configurações para trabalhar com VLANs usando portas trunk — ideal para estudos, laboratórios em GNS3 / Packet Tracer ou aplicação em equipamentos reais. Aqui você encontrará snippets de configuração, topologias e dicas para validar o tráfego entre VLANs via trunk. 🧩

## 📚 O que é este projeto
- Exemplos práticos de configuração de VLANs e portas trunk.
- Comandos e verificações para switches (ex.: Cisco IOS).
- Sugestões de topologias para testes em simuladores e ambientes reais.

## 📁 Estrutura (exemplo)
- configs/ — arquivos de configuração de switch e roteador
- topologias/ — diagramas ou descrições de topologia
- scripts/ — scripts auxiliares (se houver)
- README.md — este arquivo

> Obs.: adapte a estrutura conforme o que já existe no repositório.

## 🔧 Pré-requisitos
- Um simulador (GNS3, Cisco Packet Tracer) ou switches físicos compatíveis.
- Acesso ao CLI do switch/roteador.
- Conhecimentos básicos de redes e VLANs.

## 🚀 Exemplo rápido (Cisco IOS)
Exemplo de configuração de uma trunk entre SwitchA e SwitchB, permitindo VLANs 10 e 20:

```shell
!-- No SwitchA (interface connecting to SwitchB)
interface GigabitEthernet0/1
 description Link to SwitchB
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown

!-- No SwitchB (interface connecting to SwitchA)
interface GigabitEthernet0/1
 description Link to SwitchA
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown
```

Criando e configurando VLANs e portas de acesso:
```shell
vlan 10
 name SERVIDORES
vlan 20
 name CLIENTES

interface GigabitEthernet0/2
 description Access to Server
 switchport mode access
 switchport access vlan 10
 no shutdown

interface GigabitEthernet0/3
 description Access to Client
 switchport mode access
 switchport access vlan 20
 no shutdown
```

## ✅ Como validar / testar
- Verifique trunk ativo:
  show interfaces trunk
- Verifique VLANs configuradas:
  show vlan brief
- Teste conectividade:
  - Em cada VLAN, atribua IPs às máquinas virtuais/hosts e faça ping entre hosts da mesma VLAN.
  - Teste isolamento: hosts de VLANs diferentes não devem se comunicar sem roteamento.
- Se utilizar roteamento inter-VLAN: configure subinterfaces no roteador (router-on-a-stick) ou um SVI (switch virtual interface) e teste comunicação entre VLANs.

## 🧠 Boas práticas
- Evite usar VLAN nativa com tráfego não confiável — prefira trunk native explicitamente documentada.
- Controle as VLANs permitidas no trunk (switchport trunk allowed vlan ...) para reduzir blast domain.
- Utilize nomes de VLANs claros para facilitar manutenção.
- Proteja portas não usadas (shutdown, port-security).

## ✍️ Contribuições
Contribuições são bem-vindas! Abra uma issue para discutir mudanças ou envie um PR com:
- documentação/explicações adicionais
- novas topologias
- exemplos para outros vendors (HP, Juniper, etc.)

## 📞 Autor / Contato
- Criado por: leandroFilipy 👨‍💻
- GitHub: https://github.com/leandroFilipy

## 📄 Licença
Consulte o arquivo LICENSE no repositório. Se não houver licença, considere adicionar uma (ex.: MIT) para facilitar contribuições. ⚖️

---

Se quiser, eu posso:
- Gerar um diagrama de topologia em ASCII ou mermaid 🗺️
- Adicionar exemplos para roteamento inter-VLAN (router-on-a-stick) 🔁
- Traduzir comandos para outros vendors (Juniper, MikroTik, etc.) 🔁

Diga o que prefere e eu ajusto o README! ✨
