---
layout: post
title: "Java streams examples"
description: "flatmap, map, max, min java streams examples"
tags: [example, Java, streams]
categories: [Java, examples]
---

flatmap, map, max, min java streams examples

Let's create Team class. 

{% highlight java %}
public class Team {

    private String name;
    private Country country;

    private List<ClubWorldCup> clubWorldCupList;

    public Team(String name, List<ClubWorldCup> clubWorldCups, Country country) {
        this.name = name;
        this.clubWorldCupList = clubWorldCups;
        this.country = country;
    }
	
	//getters, setters
  }

{% endhighlight %}


and ClubWorldCup class

{% highlight java %}

public class ClubWorldCup {

    private Integer year;

    public ClubWorldCup(int year) {
        this.year = year;
    }
	
	//getters, setters
}

{% endhighlight %}

and Country enum

{% highlight java %}

public enum Country {

    SPAIN("Spain"),
    GERMANY("Germany");

    private final String name;

    Country(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

{% endhighlight %}

Creating some teams and adding them to list.

{% highlight java %}

List<Integer> yearsRealMadridChampion = Arrays.asList(2014, 2016, 2017, 2018);
Team realMadridCF = new Team("Real Madrid CF", getClubWorldCups(yearsRealMadridChampion), Country.SPAIN);
	
List<Integer> yearsBarcelonaChampion = Arrays.asList(2009, 2011, 2015);
Team barcelonaFC = new Team("FC Barcelona", getClubWorldCups(yearsBarcelonaChampion), Country.SPAIN);
	
Team fcBayernMunich = new Team("FC Bayern Munich", Arrays.asList(new ClubWorldCup(2013)), Country.GERMANY);
	
List<Team> teamList = Arrays.asList(realMadridCF, barcelonaFC, fcBayernMunich);

{% endhighlight %}

getClubWorldCups method: 

{% highlight java %}
private static List<ClubWorldCup> getClubWorldCups(List<Integer> years) {
        return years.stream().map(year -> new ClubWorldCup(year)).collect(Collectors.toList());
    }
	
{% endhighlight %}


Getting years with champions from Germany. 

{% highlight java %}
List<Integer> yearsWithGermanChampion = getChampionsYearByCountry(teamList, Country.GERMANY);
yearsWithGermanChampion.forEach(System.out::println);
{% endhighlight %}

Output:

{% highlight java %}
2013
{% endhighlight %}

Getting years with champions from Spain. 

{% highlight java %}
List<Integer> yearsWithSpainChampion = getChampionsYearByCountry(teamList, Country.SPAIN);
yearsWithSpainChampion.forEach(System.out::println);
{% endhighlight %}

Output:
{% highlight java %}
2014
2016
2017
2018
2009
2011
2015
{% endhighlight %}

getChampionsYearByCountry method

{% highlight java %}
private static List<Integer> getChampionsYearByCountry(List<Team> teamList, Country country) {
        return teamList.stream().filter(team -> country.equals(team.getCountry()))
                .flatMap(team -> team.getClubWorldCupList().stream())
                .map(cup -> cup.getYear()).collect(Collectors.toList());
    }
{% endhighlight %}

Most times champion

{% highlight java %}
Team mostTimesChampion = teamList.stream().max(Comparator.comparingInt(item->item.getClubWorldCupList().size())).get();
System.out.println(mostTimesChampion.getName());
{% endhighlight %}

Output: 

{% highlight java%}
Real Madrid CF
{% endhighlight %}

Less times champion
{% highlight java %}
Team lessTimesChampion = teamList.stream().min(Comparator.comparingInt(team->team.getClubWorldCupList().size())).get();
System.out.println(lessTimesChampion.getName());
{% endhighlight %}

Output: 

{% highlight java%}
FC Bayern Munich
{% endhighlight %}


Github link: 
<https://github.com/diegof00/java-examples.git>