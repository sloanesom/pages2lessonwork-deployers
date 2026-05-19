---
layout: post
courses: { csse: {week: 4}, csp: {week: 13}, csa: {week: 17 } }
codemirror: true
breadcrumb: True
title: CPT Guide - Code Runner
description: Build a lesson using multiple code runners on a page.  This modular approach allows you to create interactive lessons, more code -- less words.
permalink: /cpt/code
---

## CPT Guide - Code Runner
The Create Performance Task (CPT) requires a program that demonstrates core computational thinking concepts.

Your program must include:

- Input: user interaction
- Output: program-generated result
- List: collection of data items
- Procedure: reusable function with parameter
- Algorithm: sequencing, selection, iteration

## CPT Guide Home

<div style="display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 20px;">
  <a href="https://sloanesom.github.io/pages2lessonwork-deployers/cpt/code" style="text-decoration: none;">
    <div style="background-color: rgb(32, 122, 201); color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold;">
      Code Runner Guide
    </div>
  </a>
</div>

## CPT Components Draft
{% capture challenge1 %}
Pick a Language to start drafting your CPT
{% endcapture %}

{% include code-runner.html
   runner_id="exercise1"
   language="python"
   challenge=challenge1
   code=code1
%}

## Input

{% capture challenge2 %}
Complete the function to calculate the area of a rectangle. Replace the ??? with the correct calculation.
{% endcapture %}

{% capture code2 %}
def calculate_area(length, width):
    # Replace ??? with the correct formula
    area = ???
    return area
''' Test calculate area function '''
print(calculate_area(5, 3))
print(calculate_area(10, 2))
{% endcapture %}

{% include code-runner.html
   runner_id="exercise2"
   language="python"
   challenge=challenge2
   code=code2
   height="350px"
%}

## Output

{% capture challenge2 %}
Complete the function to calculate the area of a rectangle. Replace the ??? with the correct calculation.
{% endcapture %}

{% capture code2 %}
def calculate_area(length, width):
    # Replace ??? with the correct formula
    area = ???
    return area
''' Test calculate area function '''
print(calculate_area(5, 3))
print(calculate_area(10, 2))
{% endcapture %}

{% include code-runner.html
   runner_id="exercise2"
   language="python"
   challenge=challenge2
   code=code2
   height="350px"
%}

## List

{% capture challenge2 %}
Complete the function to calculate the area of a rectangle. Replace the ??? with the correct calculation.
{% endcapture %}

{% capture code2 %}
def calculate_area(length, width):
    # Replace ??? with the correct formula
    area = ???
    return area
''' Test calculate area function '''
print(calculate_area(5, 3))
print(calculate_area(10, 2))
{% endcapture %}

{% include code-runner.html
   runner_id="exercise2"
   language="python"
   challenge=challenge2
   code=code2
   height="350px"
%}

## Procedure

{% capture challenge2 %}
Complete the function to calculate the area of a rectangle. Replace the ??? with the correct calculation.
{% endcapture %}

{% capture code2 %}
def calculate_area(length, width):
    # Replace ??? with the correct formula
    area = ???
    return area
''' Test calculate area function '''
print(calculate_area(5, 3))
print(calculate_area(10, 2))
{% endcapture %}

{% include code-runner.html
   runner_id="exercise2"
   language="python"
   challenge=challenge2
   code=code2
   height="350px"
%}

## Algorithim

{% capture challenge2 %}
Complete the function to calculate the area of a rectangle. Replace the ??? with the correct calculation.
{% endcapture %}

{% capture code2 %}
def calculate_area(length, width):
    # Replace ??? with the correct formula
    area = ???
    return area
''' Test calculate area function '''
print(calculate_area(5, 3))
print(calculate_area(10, 2))
{% endcapture %}

{% include code-runner.html
   runner_id="exercise2"
   language="python"
   challenge=challenge2
   code=code2
   height="350px"
%}

## CPT Backend Draft
{% capture challenge1 %}
Pick a Language to start drafting your CPT
{% endcapture %}

{% include code-runner.html
   runner_id="exercise1"
   language="python"
   challenge=challenge1
   code=code1
%}
