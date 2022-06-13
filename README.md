# Merge DataFrame using Python e Power BI
1 - Adicionar uma tabela vazia
2 - Menu transformar do power bi /  Executar script python
3 - Referenciar o nome das tabelas que voce deseja usar em seus datasets
4 - Executar o script python desejado para gerar um novo dataset.

# Transformar coluna de Data
É necesário transformar as colunas de tata para texto para que o Power BI não as transforme em um objeto próprio reconhecido somente pelo PBI.


# Script para fazer merge nos datasets
# Merge data Python:
        import pandas as pd

        df2.drop_duplicates(subset=['Código'], keep='first', inplace=True)
        df3 = pd.merge(df1, df2.iloc[:, [0, 2, 3, 4, 5]], how='left', left_on=['Código'], right_on=['Código'])
        
# Script completo
        let
            Fonte = Table.FromRows(Json.Document(Binary.Decompress(Binary.FromText("i44FAA==", BinaryEncoding.Base64), Compression.Deflate)), let _t = ((type nullable text) meta [Serialized.Text = true]) in type table [#"Coluna 1" = _t]),
            #"Tipo Alterado" = Table.TransformColumnTypes(Fonte,{{"Coluna 1", type text}}),
            #"Executar script Python" = Python.Execute("# Merge data Python:#(lf)import pandas as pd#(lf)#(lf)df2.drop_duplicates(subset=['Código'], keep='first', inplace=True)#(lf)df3 = pd.merge(df1, df2.iloc[:, [0, 2, 3, 4, 5]], how='left', left_on=['Código'], right_on=['Código'])",[df1=Tabela1, df2=Tabela2]),
            df3 = #"Executar script Python"{[Name="df3"]}[Value]
        in
            #"Executar script Python"
