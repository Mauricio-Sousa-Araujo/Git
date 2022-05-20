# Git

## Comandos Básicos de configuração

#### Para listas configurações correntes
1. git config --list 

#### Alterar Nome Global
2. git config --global user.name "Mauricio de Sousa"

#### Alterar nome Global
3. git config --global user.name "Mauricio de Sousa"

#### Alterar nome repositório local
4. git config  user.name "Mauricio de Sousa"

#### Alterar e-mail  global
5.  git config --global user.email "mauricio_ploc@hotmail.com"

#### Alterar e-mail repositório local
6.  git config  user.email "mauricio_ploc@hotmail.com"


## Comandos Básicos de trabalho

#### Cria o arquivo .git para que o arquivo possa ser versionado
1. git init  

#### Adiciona o arquivo para área de staging
2. git add file_name

#### Salva os arquivos da área de staging para o repositório local
3. git commit -m "Mensagem de comite"

#### 
4. git diff

#### 
5.  git diff -staged


## Comandos de log


#### Mostra histórico de  comites do mais recente pro mais antigo
1.  git log

#### Mostra histórico de  comites do mais recente pro mais antigo
2. git checkout id_versão

#### Limpa arquivos que foram criados que ainda não estão na área de staged
3. git clean -f

#### Remove as alterações que estão em stage
4. git reset --hard == git restore archive

#### Puxa alterações do repositório remoto
5. git pull

#### Empurra alterações no repositório remoto
4. git push






























explain 
with RANK_STAGE as
(
select  *
		,coalesce (sh.dt_segmento, ph.dt_posicao) as dt
		,coalesce (sh.cpf, ph.cpf) as cpf_cnpj
		,case 
			when gerente is null then '0'		
			else CAST( row_number() over (partition by coalesce (sh.cpf, ph.cpf) order by coalesce (sh.dt_segmento, ph.dt_posicao)) as varchar )
		 end row_number 
from "Posicao_hist" ph  
	 	full outer join 
	 "Seg_hist" sh  
on sh.cpf = ph.cpf and sh.dt_segmento = ph.dt_posicao 
), CONCAT_ROW_NUMBER as
(select *
		,concat( lpad( row_number ,12, '0'), gerente) as gerente_row_number
from RANK_STAGE
), final as
(
select *
	   , substring(max(gerente_row_number) over (partition by cpf_cnpj order by dt 
	   								   rows between unbounded preceding and current row ),13) as gerente_fill
	   
from CONCAT_ROW_NUMBER)
select *
from final
where dt_posicao is not null;





/*outraaaaaaaaaaaaaaaaaaaaaaaa*/
explain with POSICAO_SEGMENTACAO as (
		select  *
				,coalesce (sh.dt_segmento, ph.dt_posicao) as dt
				,row_number () over (partition by  ph.dt_posicao, ph.cpf  order by sh.dt_segmento DESC)
		from "Posicao_hist" ph  
			 	join 
			 "Seg_hist" sh  
		on sh.cpf = ph.cpf and ph.dt_posicao >= sh.dt_segmento  
)
select *
from  POSICAO_SEGMENTACAO
where row_number = 1;
