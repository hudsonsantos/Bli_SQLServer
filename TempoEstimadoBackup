-- Mostra o tempo estimado para término de um backup

-- Note que nela temos as seguintes informações sobre execução:
-- Hora de início (start_time)
-- Tempo decorrido (MinutesRunning),
-- Percentual exato da operação (percent_complete)
-- Tempo estimado para conclusão (MinutesToFinish)



SELECT start_time,
       (total_elapsed_time/1000/60) AS MinutesRunning,
       percent_complete,
       command,
       b.name AS DatabaseName,
              -- MASTER will appear here because the database is not accesible yet.
       DATEADD(ms,estimated_completion_time,GETDATE()) AS StimatedCompletionTime,
      (estimated_completion_time/1000/60) AS MinutesToFinish
FROM  sys.dm_exec_requests a
          INNER JOIN sys.databases b ON a.database_id = b.database_id
WHERE command LIKE '%restore%'
          OR command LIKE '%backup%'
          AND estimated_completion_time > 0
