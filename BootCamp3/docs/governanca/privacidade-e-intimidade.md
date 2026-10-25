# Privacidade, intimidade e proteção de dados

**Objetivo:** estabelecer salvaguardas proporcionais ao projeto acadêmico. Este documento é uma orientação operacional e não substitui avaliação jurídica nem a política institucional.

## Princípios de tratamento

1. **Minimização:** o validador recebe apenas uma string e não precisa de nome, CPF, endereço, localização, imagem ou dados do proprietário.
2. **Finalidade e necessidade:** usar entradas sintéticas para desenvolvimento, testes, demonstrações e relatórios. Não consultar nem armazenar dados reais de veículos.
3. **Privacidade por padrão:** não adicionar logs do conteúdo completo da placa sem necessidade aprovada; preferir registrar status, duração e identificador técnico não identificável.
4. **Acesso mínimo:** acesso ao repositório e às configurações administrativas limitado aos integrantes que precisam dele.
5. **Transparência:** explicar que a aplicação valida apenas o formato e não confirma existência, titularidade, regularidade, multas ou roubo/furto.
6. **Segurança:** não versionar `.env`, tokens, chaves, credenciais, dumps, logs ou capturas com dados pessoais. Usar segredos do ambiente/CI.
7. **Retenção limitada:** remover dados de teste acidentais e artefatos de execução quando não forem mais necessários, respeitando as regras institucionais e os requisitos de preservação de evidências.
8. **Revisão humana:** avaliar dependências, código gerado por IA e serviços externos antes de compartilhar dados ou integrar alterações.

## Placa e dado pessoal

Uma placa isolada não é automaticamente dado pessoal em qualquer contexto. Porém, quando pode ser associada a uma pessoa natural, seu uso pode envolver dado pessoal e requer avaliação contextual. Para este projeto, a política segura é **não usar placas reais**. Exemplos como `ABC1234` e `ABC1D23` são fictícios e devem ser tratados como exemplos sintéticos.

## Direitos e solicitações

Quando houver tratamento de dados pessoais no contexto do projeto, encaminhar solicitações ao responsável institucional ou controlador competente. Conforme a aplicabilidade da LGPD, os direitos podem incluir confirmação da existência de tratamento, acesso, correção, anonimização/bloqueio/eliminação de dados desnecessários ou tratados em desconformidade e informações sobre compartilhamento. A aplicabilidade, os prazos e eventuais exceções devem ser avaliados pelo responsável competente.

O direito à privacidade e à intimidade deve ser respeitado em documentação, issues, comentários, demonstrações, capturas de tela e relatórios. Não publicar dados pessoais de integrantes além do estritamente necessário e autorizado; evitar números de matrícula/RA em artefatos públicos se não forem exigidos.

## Incidente ou exposição acidental

1. Não reproduzir o segredo/dado na Issue ou no relatório.
2. Avisar imediatamente o mantenedor e o responsável institucional, usando canal privado.
3. Revogar/rotacionar credenciais expostas; remover o dado do código atual e do histórico quando necessário, reconhecendo que apagar um commit não garante remoção de cópias.
4. Identificar escopo, período, sistemas e pessoas potencialmente afetadas, sem especulação.
5. Registrar ações e horários sem copiar o dado sensível.
6. O controlador/responsável avalia obrigações de comunicação e medidas cabíveis.
7. Criar uma Issue sanitizada para a correção técnica e registrar a conclusão.

## Checklist obrigatório de PR

- [ ] Apenas dados sintéticos em exemplos, testes e documentação.
- [ ] Nenhuma credencial, token, chave, `.env`, log sensível ou dump incluído.
- [ ] Logs não revelam entrada integral sem justificativa.
- [ ] Dependências e serviços externos foram avaliados.
- [ ] O README deixa claros os limites do validador.
- [ ] Qualquer exceção à política foi justificada e aprovada pelo responsável.
