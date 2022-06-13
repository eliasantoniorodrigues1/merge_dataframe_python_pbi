# Merge DataFrame using Python e Power BI
1 - Adicionar uma tabela vazia

2 - Menu transformar do power bi /  Executar script python

3 - Referenciar o nome das tabelas que voce deseja usar em seus datasets

4 - Executar o script python desejado para gerar um novo dataset.


# Transformar coluna de Data
É necesário transformar as colunas de tata para texto para que o Power BI não as transforme em um objeto próprio reconhecido somente pelo PBI.

# Tabela vazia após a adicao da etapa "Executa script python"
        = Python.Execute("# Merge data Python:",[df1=Tabela1, df2=Tabela2])

# Imagem de como a tabela vazia vai ficar apos referenciar as tabelas:
![image](https://user-images.githubusercontent.com/49626719/173365663-dfb365a4-a306-4f6c-84ef-e60ee5ae130f.png)


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
            
# Fonte StackOverflow:
How to use python with multiple tables in the Power query editor?(https://stackoverflow.com/questions/51947441/power-bi-how-to-use-python-with-multiple-tables-in-the-power-query-editor)
