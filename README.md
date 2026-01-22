# Email Server c/ Postfix, Dovecot e LDAP

Este repositório contém o trabalho desenvolvido no âmbito da unidade curricular **Serviços de Rede II (SR2)** do **ISEC**, no ano letivo **2025/2026**.

## Objetivo do Projeto

O objetivo deste projeto foi a implementação de um **sistema completo de correio eletrónico em ambiente Linux**, recorrendo a software open-source amplamente utilizado:

- **Postfix** – Mail Transfer Agent (MTA)
- **Dovecot** – Mail Delivery Agent (MDA) e servidor IMAP
- **Thunderbird** – Mail User Agent (cliente)
- **Microsoft Active Directory** – autenticação centralizada via **LDAP**

O sistema permite o envio e receção de emails por clientes remotos, com **submissão segura (SMTP Submission na porta 587 com STARTTLS)**, acesso às mailboxes via **IMAP**, e autenticação centralizada através de **Active Directory**.

## 🧱 Arquitetura do Sistema

A solução é composta por três máquinas virtuais interligadas numa LAN:

- **Cliente (Debian)**: executa o Thunderbird para envio e leitura de emails.
- **Servidor de Email (Debian)**: executa Postfix e Dovecot, sendo responsável pelo transporte, entrega e acesso ao correio.
- **Windows Server**: executa Active Directory e DNS, funcionando como base centralizada de utilizadores, acedida via LDAP.

A autenticação SMTP (SASL) é delegada pelo Postfix ao Dovecot, que por sua vez valida as credenciais localmente ou através do Active Directory.

## 🖥️ Ambiente de Implementação

Todo o sistema foi implementado e testado num ambiente virtualizado, utilizando o **Proxmox VE** como plataforma de virtualização.

Foram criadas máquinas virtuais independentes para:
- Cliente de email
- Servidor de email
- Servidor Windows (Active Directory)

Esta abordagem permitiu isolamento dos serviços, controlo da rede e replicação de um cenário próximo de um ambiente real.

## 🧪 Validação

O funcionamento do sistema foi validado através de:
- Testes de submissão SMTP (porta 587, STARTTLS e SASL)
- Testes de acesso IMAP via Thunderbird
- Análise dos logs dos serviços Postfix e Dovecot
