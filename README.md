# SQL-Data-Exploration
select *
from dbo.CovidData
Where total_cases is not null
order by 3,4

Select Location , date , total_cases , total_deaths , (total_deaths/total_cases)*100 as DeathPercentage 
from dbo.CovidData
where location like '%kingdom%'
order by 1,2

Select Location , date , population , total_deaths , (total_cases/population)*100 as DeathPercentage 
from dbo.CovidData
where location like '%kingdom%'
order by 1,2

Select Location , date , population , total_deaths , (total_cases/population)*100 as DeathPercentage 
from dbo.CovidData
order by 1,2

Select Location, Population, MAX(total_cases) as HighestInfectionCount,  Max((total_cases/population))*100 as PercentPopulationInfected
From dbo.CovidData
Group by Location, Population
order by PercentPopulationInfected desc


Select Location, MAX(cast(Total_deaths as int)) as TotalDeathCount
From dbo.CovidData
Group by Location
order by TotalDeathCount desc

Select Location, MAX(cast(Total_deaths as int)) as TotalDeathCount
From dbo.CovidData
Where continent is not null 
Group by Location
order by TotalDeathCount desc

Select continent, MAX(cast(Total_deaths as int)) as TotalDeathCount
From dbo.CovidData
Where continent is not null 
Group by continent
order by TotalDeathCount desc

Select SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) as total_deaths, SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage
From dbo.CovidData
where continent is not null 
order by 1,2

Select SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) as total_deaths, SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage
From dbo.CovidData
where continent is not null 
order by 1,2

DROP Table if exists #PercentPopulationVaccinated
Create Table #PercentPopulationVaccinated
(
Continent nvarchar(255),
Location nvarchar(255),
Date datetime,
Population numeric,
New_vaccinations numeric,
RollingPeopleVaccinated numeric
)

select * 
from dbo.CovidData
