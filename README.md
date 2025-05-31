-- Obtém o serviço de jogadores
local Players = game:GetService("Players")
local DataStoreService = game:GetService("DataStoreService")
local banDataStore = DataStoreService:GetDataStore("BanDataStore")

-- Função para banir um jogador
local function banirJogador(userId, tempo)
    -- Obtém o jogador
    local jogador = Players:GetPlayerByUserId(userId)
    
    -- Verifica se o jogador existe
    if jogador then
        -- Banir o jogador
        jogador:Kick("Você foi banido por " .. tempo .. " minutos!")
        
        -- Salva o banimento no DataStore
        banDataStore:SetAsync("Ban_" .. userId, os.time() + tempo * 60)
    end
end

-- Função para verificar se um jogador está banido
local function verificarBanimento(userId)
    local banTime = banDataStore:GetAsync("Ban_" .. userId)
    if banTime and banTime > os.time() then
        return true
    else
        return false
    end
end

-- Exemplo de uso
banirJogador(123456789, 30) -- Banir por 30 minutos
